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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>¿Cómo tooSend correo electrónico utilizando SendGrid desde Java
Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure. ejemplos de Hello están escritos en Java. Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, **agregar datos adjuntos**, **mediante filtros**y **actualizar propiedades**. Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos siguientes](#next-steps) sección.

## <a name="what-is-hello-sendgrid-email-service"></a>¿Qué es hello SendGrid servicio de correo electrónico?
SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada. Entre los escenarios de uso de SendGrid comunes se incluyen:

* Enviar automáticamente confirmaciones toocustomers
* Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes
* Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.
* Generar informes toohelp identificar tendencias
* Reenvío de consultas de los clientes
* Envío de notificaciones de correo electrónico desde su aplicación

Para obtener más información, consulte <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Creación de una cuenta de SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Cómo: usar bibliotecas de javax.mail Hola
Obtener bibliotecas de javax.mail hello, por ejemplo de <http://www.oracle.com/technetwork/java/javamail> e importarlos en el código. En un nivel superior, hello proceso para utilizar Hola javax.mail biblioteca toosend correo electrónico mediante SMTP es toodo Hola siguiente:

1. Especificar valores de SMTP de hello, incluido el servidor SMTP de hello, que para SendGrid smtp.sendgrid.net.

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

1. Extender hello *javax.mail.Authenticator* (clase) y en la implementación de la *getPasswordAuthentication* (método), devuelven el nombre de usuario de SendGrid y la contraseña.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Cree una sesión de correo electrónico autenticado a través de un objeto *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Cree su mensaje y asigne los valores **Para**, **De**, **Asunto** y los valores de contenido. Esto se muestra en hello [Cómo: crear un correo electrónico](#how-to-create-an-email) sección.
4. Enviar mensaje de Hola a través de un *javax.mail.Transport* objeto. Esto se muestra en hello [Cómo: enviar un correo electrónico] [Cómo: enviar un correo electrónico] sección.

## <a name="how-to-create-an-email"></a>Creación de un correo electrónico
siguiente Hello muestra la valoración toospecify busque un correo electrónico.

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

## <a name="how-to-send-an-email"></a>Envío de un correo electrónico
Hola siguientes se muestra cómo toosend un correo electrónico.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Incorporación de un archivo adjunto
Hello código siguiente muestra cómo tooadd datos adjuntos.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Cómo: usar filtros tooenable pies de página, el seguimiento y análisis
SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de *filtros*. Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente. Si desea obtener una lista completa de los filtros, consulte [Filter Settings][Filter Settings].

* Hola continuación, muestra cómo filtrar los tooinsert un pie de página en la que da lugar a texto HTML que aparece en la parte inferior de Hola de correo electrónico de Hola que se envían.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Otro ejemplo de un filtro es el seguimiento de clics. Supongamos que el texto de correo electrónico contiene un hipervínculo, como hello siguiente y desea que tootrack hello, haga clic en velocidad:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* Hola tooenable haga clic en seguimiento Hola de uso siguiente código:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Actualización de las propiedades del correo electrónico
Algunas propiedades de correo electrónico se pueden sobrescribir con  **establecer*propiedad*** o estar anexados mediante  **agregar*propiedad***.

Por ejemplo, toospecify **ReplyTo** direcciones, utilice el siguiente de hello:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd una **Cc** siguiente de Hola de destinatario, use:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Uso de servicios adicionales de SendGrid
SendGrid ofrece API basadas en web que puede usar la funcionalidad adicional de SendGrid de tooleverage desde la aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.

* Ejemplo que muestra cómo utilizar SendGrid en una implementación de Azure: [cómo toosend de correo electrónico con SendGrid desde Java en una implementación de Azure](store-sendgrid-java-how-to-send-email-example.md)
* SDK de Java de SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html>
* Documentación sobre la API de SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Oferta especial de SendGrid para clientes de Azure: <https://sendgrid.com/windowsazure.html>

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
