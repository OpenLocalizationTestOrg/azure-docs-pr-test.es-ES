---
title: "aaaHow toouse Hola servicio de correo electrónico de SendGrid (. NET) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico de SendGrid hello en Azure. Ejemplos de código escritos en C# y el uso de hello .NET API."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Cómo tooSend SendGrid de uso de correo electrónico con Azure
## <a name="overview"></a>Información general
Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure. Hola ejemplos están escritos en C\# y es compatible con .NET estándar 1.3. escenarios de Hello descritos incluyen crear correo electrónico, enviar correo electrónico, agregar datos adjuntos y habilitar correo electrónico distintos y configuración del seguimiento. Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos siguientes] [ Next steps] sección.

## <a name="what-is-hello-sendgrid-email-service"></a>¿Qué es hello SendGrid servicio de correo electrónico?
SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada. A continuación se indican casos de uso comunes de SendGrid:

* Enviar automáticamente confirmaciones o toocustomers de confirmaciones de compra.
* Administración de las listas de distribución para el envío mensual de folletos y promociones a clientes.
* Recopilación de métricas en tiempo real para, por ejemplo, direcciones de correo electrónico bloqueadas y captación de clientes.
* Reenvío de las consultas de los clientes.
* Procesamiento de mensajes de correo electrónico entrantes.

Para más información, visite [https://sendgrid.com](https://sendgrid.com) o el repositorio de GitHub de la [biblioteca de C# ][sendgrid-csharp] de SendGrid.

## <a name="create-a-sendgrid-account"></a>Creación de una cuenta de SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Hacer referencia a Hola biblioteca de clases de .NET de SendGrid
Hola [paquete SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) es hello tooget de manera más fácil de hello API de SendGrid y tooconfigure la aplicación con todas las dependencias. NuGet es un extensión incluido con Microsoft Visual Studio 2015 y posterior que resulta herramientas y bibliotecas fácil de tooinstall y actualización de Visual Studio.

> [!NOTE]
> tooinstall NuGet si está ejecutando una versión de Visual Studio anteriores a Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)y haga clic en hello **instalar NuGet** botón.
>
>

Hola tooinstall el paquete SendGrid NuGet en la aplicación Hola siguientes:

1. Haga clic en **Nuevo proyecto** y seleccione una **Plantilla**.

   ![Crear un nuevo proyecto][create-new-project]
2. En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** y, después, en **Administrar paquetes NuGet**.

   ![paquete NuGet de SendGrid][SendGrid-NuGet-package]
3. Busque **SendGrid** y seleccione hello **SendGrid** elemento de la lista de resultados.
4. Seleccione versión estable más reciente de Hola de paquete de Nuget Hola de hello versión desplegable toobe puede toowork con el modelo de objetos de Hola y las API que se muestra en este artículo.

   ![Paquete de SendGrid][sendgrid-package]
5. Haga clic en **instalar** toocomplete Hola instalación y, a continuación, cierre este cuadro de diálogo.

La biblioteca de clases .NET de SendGrid se llama **SendGrid**. Contiene Hola después de los espacios de nombres:

* **SendGrid** para comunicarse con la API de SendGrid.
* **SendGrid.Helpers.Mail** para la aplicación auxiliar métodos tooeasily crear objetos SendGridMessage que especifican cómo toosend envía por correo electrónico.

Agregar Hola después código espacio de nombres declaraciones toohello parte superior de cualquier archivo de C# en el que desea que el servicio de correo electrónico de tooprogrammatically acceso hello SendGrid.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Creación de un correo electrónico
Hola de uso **SendGridMessage** toocreate un mensaje de correo electrónico del objeto. Una vez que se crea el objeto de mensaje de Hola, puede establecer las propiedades y métodos, incluido el remitente del correo electrónico Hola, destinatario de correo electrónico de Hola y Hola asunto y al cuerpo del correo electrónico de Hola.

Hello ejemplo siguiente se muestra cómo toocreate un objeto totalmente rellenada de correo electrónico:

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

Para más información sobre las propiedades y los métodos que admite el tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] en GitHub.

## <a name="how-to-send-an-email"></a>Envío de un correo electrónico
Después de crear un mensaje de correo electrónico, puede enviarlo con la API de SendGrid. También puede usar la [biblioteca integrada de .NET][NET-library].

El envío de correos electrónicos requiere que el usuario proporcione su clave de API de SendGrid. Si necesita obtener más información acerca de cómo tooconfigure claves de API, visite las claves de API de SendGrid [documentación][documentation].

Puede almacenar estas credenciales a través de su Portal de Azure, haga clic en configuración de la aplicación y agregar pares de clave/valor de hello en configuración de la aplicación.

 ![Configuración de la aplicación de Azure][azure_app_settings]

 A continuación, puede tener acceso a ellas de la siguiente manera:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Hello en los ejemplos siguientes muestra cómo toosend un mensaje mediante Hola API Web.

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a>Incorporación de un archivo adjunto
Los datos adjuntos pueden agregar tooa mensaje Hola llamada **AddAttachment** método y mínimamente especificando el nombre del archivo de Hola y con codificación Base64 de contenido desean tooattach. Puede incluir varios archivos adjuntos mediante una llamada a este método una vez para cada archivo que se va tooattach o mediante el uso de hello **AddAttachments** método. Hola de ejemplo siguiente se muestra cómo agregar un mensaje de tooa de datos adjuntos:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Cómo: usar pies de página de tooenable de configuración de correo electrónico, el seguimiento y análisis
SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de configuración de correo electrónico y la configuración de seguimiento. Estas opciones se pueden agregar tooan correo electrónico mensaje tooenable funcionalidad específica, como el seguimiento de clics, Google analytics, seguimiento de suscripción y así sucesivamente. Para obtener una lista completa de las aplicaciones, vea hello [documentación de la configuración][settings-documentation].

Las aplicaciones pueden aplicarse demasiado**SendGrid** mediante los métodos implementados como parte del programa Hola de mensajes de correo electrónico **SendGridMessage** clase. Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:

Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:

### <a name="footer-settings"></a>Configuración de pie de página
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Seguimiento por clics
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Uso de servicios adicionales de SendGrid
SendGrid ofrece varias API y webhooks, que puede usar una funcionalidad adicional tooleverage dentro de la aplicación de Azure. Para obtener más información, vea hello [referencia de la API de SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.

* Repositorio de bibliotecas de C#\# de SendGrid: [sendgrid-csharp][sendgrid-csharp]
* Documentación sobre la API de SendGrid: <https://sendgrid.com/docs>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[servicio de correo electrónico basado en la nube]: https://sendgrid.com/solutions
[entrega de correo electrónico transaccional]: https://sendgrid.com/use-cases/transactional-email

