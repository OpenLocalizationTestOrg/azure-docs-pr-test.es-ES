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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="9dc7e-104">Cómo tooSend SendGrid de uso de correo electrónico con Azure</span><span class="sxs-lookup"><span data-stu-id="9dc7e-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="9dc7e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="9dc7e-105">Overview</span></span>
<span data-ttu-id="9dc7e-106">Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="9dc7e-107">Hola ejemplos están escritos en C\# y es compatible con .NET estándar 1.3.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="9dc7e-108">escenarios de Hello descritos incluyen crear correo electrónico, enviar correo electrónico, agregar datos adjuntos y habilitar correo electrónico distintos y configuración del seguimiento.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="9dc7e-109">Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos siguientes] [ Next steps] sección.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="9dc7e-110">¿Qué es hello SendGrid servicio de correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="9dc7e-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="9dc7e-111">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="9dc7e-112">A continuación se indican casos de uso comunes de SendGrid:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="9dc7e-113">Enviar automáticamente confirmaciones o toocustomers de confirmaciones de compra.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="9dc7e-114">Administración de las listas de distribución para el envío mensual de folletos y promociones a clientes.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="9dc7e-115">Recopilación de métricas en tiempo real para, por ejemplo, direcciones de correo electrónico bloqueadas y captación de clientes.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="9dc7e-116">Reenvío de las consultas de los clientes.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="9dc7e-117">Procesamiento de mensajes de correo electrónico entrantes.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-117">Processing incoming emails.</span></span>

<span data-ttu-id="9dc7e-118">Para más información, visite [https://sendgrid.com](https://sendgrid.com) o el repositorio de GitHub de la [biblioteca de C# ][sendgrid-csharp] de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="9dc7e-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="9dc7e-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="9dc7e-120">Hacer referencia a Hola biblioteca de clases de .NET de SendGrid</span><span class="sxs-lookup"><span data-stu-id="9dc7e-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="9dc7e-121">Hola [paquete SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) es hello tooget de manera más fácil de hello API de SendGrid y tooconfigure la aplicación con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="9dc7e-122">NuGet es un extensión incluido con Microsoft Visual Studio 2015 y posterior que resulta herramientas y bibliotecas fácil de tooinstall y actualización de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="9dc7e-123">tooinstall NuGet si está ejecutando una versión de Visual Studio anteriores a Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)y haga clic en hello **instalar NuGet** botón.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="9dc7e-124">Hola tooinstall el paquete SendGrid NuGet en la aplicación Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="9dc7e-125">Haga clic en **Nuevo proyecto** y seleccione una **Plantilla**.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-125">Click on **New Project** and select a **Template**.</span></span>

   ![Crear un nuevo proyecto][create-new-project]
2. <span data-ttu-id="9dc7e-127">En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** y, después, en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![paquete NuGet de SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="9dc7e-129">Busque **SendGrid** y seleccione hello **SendGrid** elemento de la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="9dc7e-130">Seleccione versión estable más reciente de Hola de paquete de Nuget Hola de hello versión desplegable toobe puede toowork con el modelo de objetos de Hola y las API que se muestra en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Paquete de SendGrid][sendgrid-package]
5. <span data-ttu-id="9dc7e-132">Haga clic en **instalar** toocomplete Hola instalación y, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="9dc7e-133">La biblioteca de clases .NET de SendGrid se llama **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="9dc7e-134">Contiene Hola después de los espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="9dc7e-135">**SendGrid** para comunicarse con la API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="9dc7e-136">**SendGrid.Helpers.Mail** para la aplicación auxiliar métodos tooeasily crear objetos SendGridMessage que especifican cómo toosend envía por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="9dc7e-137">Agregar Hola después código espacio de nombres declaraciones toohello parte superior de cualquier archivo de C# en el que desea que el servicio de correo electrónico de tooprogrammatically acceso hello SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="9dc7e-138">Creación de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="9dc7e-138">How to: Create an Email</span></span>
<span data-ttu-id="9dc7e-139">Hola de uso **SendGridMessage** toocreate un mensaje de correo electrónico del objeto.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="9dc7e-140">Una vez que se crea el objeto de mensaje de Hola, puede establecer las propiedades y métodos, incluido el remitente del correo electrónico Hola, destinatario de correo electrónico de Hola y Hola asunto y al cuerpo del correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="9dc7e-141">Hello ejemplo siguiente se muestra cómo toocreate un objeto totalmente rellenada de correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

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

<span data-ttu-id="9dc7e-142">Para más información sobre las propiedades y los métodos que admite el tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="9dc7e-143">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="9dc7e-143">How to: Send an Email</span></span>
<span data-ttu-id="9dc7e-144">Después de crear un mensaje de correo electrónico, puede enviarlo con la API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="9dc7e-145">También puede usar la [biblioteca integrada de .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="9dc7e-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="9dc7e-146">El envío de correos electrónicos requiere que el usuario proporcione su clave de API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="9dc7e-147">Si necesita obtener más información acerca de cómo tooconfigure claves de API, visite las claves de API de SendGrid [documentación][documentation].</span><span class="sxs-lookup"><span data-stu-id="9dc7e-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="9dc7e-148">Puede almacenar estas credenciales a través de su Portal de Azure, haga clic en configuración de la aplicación y agregar pares de clave/valor de hello en configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Configuración de la aplicación de Azure][azure_app_settings]

 <span data-ttu-id="9dc7e-150">A continuación, puede tener acceso a ellas de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="9dc7e-151">Hello en los ejemplos siguientes muestra cómo toosend un mensaje mediante Hola API Web.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-151">hello following examples show how toosend a message using hello Web API.</span></span>

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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="9dc7e-152">Incorporación de un archivo adjunto</span><span class="sxs-lookup"><span data-stu-id="9dc7e-152">How to: Add an attachment</span></span>
<span data-ttu-id="9dc7e-153">Los datos adjuntos pueden agregar tooa mensaje Hola llamada **AddAttachment** método y mínimamente especificando el nombre del archivo de Hola y con codificación Base64 de contenido desean tooattach.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="9dc7e-154">Puede incluir varios archivos adjuntos mediante una llamada a este método una vez para cada archivo que se va tooattach o mediante el uso de hello **AddAttachments** método.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="9dc7e-155">Hola de ejemplo siguiente se muestra cómo agregar un mensaje de tooa de datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="9dc7e-156">Cómo: usar pies de página de tooenable de configuración de correo electrónico, el seguimiento y análisis</span><span class="sxs-lookup"><span data-stu-id="9dc7e-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="9dc7e-157">SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de configuración de correo electrónico y la configuración de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="9dc7e-158">Estas opciones se pueden agregar tooan correo electrónico mensaje tooenable funcionalidad específica, como el seguimiento de clics, Google analytics, seguimiento de suscripción y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="9dc7e-159">Para obtener una lista completa de las aplicaciones, vea hello [documentación de la configuración][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="9dc7e-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="9dc7e-160">Las aplicaciones pueden aplicarse demasiado**SendGrid** mediante los métodos implementados como parte del programa Hola de mensajes de correo electrónico **SendGridMessage** clase.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="9dc7e-161">Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="9dc7e-162">Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="9dc7e-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="9dc7e-163">Configuración de pie de página</span><span class="sxs-lookup"><span data-stu-id="9dc7e-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="9dc7e-164">Seguimiento por clics</span><span class="sxs-lookup"><span data-stu-id="9dc7e-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="9dc7e-165">Uso de servicios adicionales de SendGrid</span><span class="sxs-lookup"><span data-stu-id="9dc7e-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="9dc7e-166">SendGrid ofrece varias API y webhooks, que puede usar una funcionalidad adicional tooleverage dentro de la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="9dc7e-167">Para obtener más información, vea hello [referencia de la API de SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="9dc7e-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dc7e-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9dc7e-168">Next steps</span></span>
<span data-ttu-id="9dc7e-169">Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="9dc7e-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="9dc7e-170">Repositorio de bibliotecas de C#\# de SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="9dc7e-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="9dc7e-171">Documentación sobre la API de SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="9dc7e-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

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

