---
title: "Uso del servicio de correo electrónico SendGrid (.NET) | Microsoft Docs"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico SendGrid en Azure. Los ejemplos de código están escritos en C# y utilizan la API .NET."
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
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="89d74-104">Envío de correos electrónicos con SendGrid y Azure</span><span class="sxs-lookup"><span data-stu-id="89d74-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="89d74-105">Información general</span><span class="sxs-lookup"><span data-stu-id="89d74-105">Overview</span></span>
<span data-ttu-id="89d74-106">Esta guía describe cómo realizar tareas comunes de programación con el servicio de correo electrónico SendGrid en Azure.</span><span class="sxs-lookup"><span data-stu-id="89d74-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="89d74-107">Los ejemplos están escritos en C\# y admiten .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="89d74-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="89d74-108">Entre los escenarios descritos se incluyen creación de correos electrónicos, envío de correos electrónicos, incorporación de datos adjuntos y habilitación de varias configuraciones de correo y seguimiento.</span><span class="sxs-lookup"><span data-stu-id="89d74-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="89d74-109">Para más información sobre SendGrid y el envío de correo electrónico, consulte la sección [Pasos siguientes][Next steps].</span><span class="sxs-lookup"><span data-stu-id="89d74-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="89d74-110">¿Qué es el servicio de correo electrónico SendGrid?</span><span class="sxs-lookup"><span data-stu-id="89d74-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="89d74-111">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="89d74-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="89d74-112">A continuación se indican casos de uso comunes de SendGrid:</span><span class="sxs-lookup"><span data-stu-id="89d74-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="89d74-113">Envío automático de recepciones o compra de confirmaciones a clientes.</span><span class="sxs-lookup"><span data-stu-id="89d74-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="89d74-114">Administración de las listas de distribución para el envío mensual de folletos y promociones a clientes.</span><span class="sxs-lookup"><span data-stu-id="89d74-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="89d74-115">Recopilación de métricas en tiempo real para, por ejemplo, direcciones de correo electrónico bloqueadas y captación de clientes.</span><span class="sxs-lookup"><span data-stu-id="89d74-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="89d74-116">Reenvío de las consultas de los clientes.</span><span class="sxs-lookup"><span data-stu-id="89d74-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="89d74-117">Procesamiento de mensajes de correo electrónico entrantes.</span><span class="sxs-lookup"><span data-stu-id="89d74-117">Processing incoming emails.</span></span>

<span data-ttu-id="89d74-118">Para más información, visite [https://sendgrid.com](https://sendgrid.com) o el repositorio de GitHub de la [biblioteca de C# ][sendgrid-csharp] de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89d74-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="89d74-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="89d74-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="89d74-120">Referencia de la biblioteca de clases .NET de SendGrid</span><span class="sxs-lookup"><span data-stu-id="89d74-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="89d74-121">El [paquete NuGet de SendGrid](https://www.nuget.org/packages/Sendgrid) es la forma más fácil de obtener la API de SendGrid y configurar la aplicación con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="89d74-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="89d74-122">NuGet es una extensión de Visual Studio incluida en Microsoft Visual Studio 2015 y superior que facilita la instalación y la actualización de las bibliotecas y las herramientas.</span><span class="sxs-lookup"><span data-stu-id="89d74-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="89d74-123">Para instalar NuGet si ejecuta una versión de Visual Studio anterior a Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)y haga clic en el botón **Instalar NuGet** .</span><span class="sxs-lookup"><span data-stu-id="89d74-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="89d74-124">Realice los pasos siguientes para instalar el paquete NuGet de SendGrid en su aplicación:</span><span class="sxs-lookup"><span data-stu-id="89d74-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="89d74-125">Haga clic en **Nuevo proyecto** y seleccione una **Plantilla**.</span><span class="sxs-lookup"><span data-stu-id="89d74-125">Click on **New Project** and select a **Template**.</span></span>

   ![Crear un nuevo proyecto][create-new-project]
2. <span data-ttu-id="89d74-127">En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** y, después, en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="89d74-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![paquete NuGet de SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="89d74-129">Busque **SendGrid** y seleccione el elemento **SendGrid** en la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="89d74-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="89d74-130">Seleccione la versión estable más reciente del paquete de NuGet en la lista desplegable de versiones para poder trabajar con el objeto de modelo y las API que se muestran en este artículo.</span><span class="sxs-lookup"><span data-stu-id="89d74-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![Paquete de SendGrid][sendgrid-package]
5. <span data-ttu-id="89d74-132">Haga clic en **Instalar** para completar la instalación y cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89d74-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="89d74-133">La biblioteca de clases .NET de SendGrid se llama **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="89d74-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="89d74-134">Contiene los siguientes espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="89d74-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="89d74-135">**SendGrid** para comunicarse con la API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89d74-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="89d74-136">**SendGrid.Helpers.Mail** para métodos auxiliares para crear fácilmente objetos SendGridMessage que especifican cómo enviar correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="89d74-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="89d74-137">Agregue las siguientes declaraciones de espacio de nombres de código en la parte superior de todo archivo C# en el que desee obtener acceso al servicio de correo electrónico SendGrid mediante programación:</span><span class="sxs-lookup"><span data-stu-id="89d74-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="89d74-138">Creación de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="89d74-138">How to: Create an Email</span></span>
<span data-ttu-id="89d74-139">Use el objeto **SendGridMessage** para crear un mensaje de correo.</span><span class="sxs-lookup"><span data-stu-id="89d74-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="89d74-140">Una vez creado el objeto de mensaje, establecer propiedades y métodos, incluidos el remitente, el destinatario, el asunto y el cuerpo del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="89d74-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="89d74-141">El siguiente ejemplo muestra la forma de crear un objeto de correo electrónico completo:</span><span class="sxs-lookup"><span data-stu-id="89d74-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="89d74-142">Para más información sobre las propiedades y los métodos que admite el tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="89d74-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="89d74-143">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="89d74-143">How to: Send an Email</span></span>
<span data-ttu-id="89d74-144">Después de crear un mensaje de correo electrónico, puede enviarlo con la API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89d74-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="89d74-145">También puede usar la [biblioteca integrada de .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="89d74-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="89d74-146">El envío de correos electrónicos requiere que el usuario proporcione su clave de API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89d74-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="89d74-147">Si desea detalles sobre cómo configurar claves de API, visite la [documentación][documentation] de claves de API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89d74-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="89d74-148">Puede almacenar estas credenciales en Azure Portal haciendo clic en Configuración de la aplicación y agregando pares clave-valor en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89d74-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Configuración de la aplicación de Azure][azure_app_settings]

 <span data-ttu-id="89d74-150">A continuación, puede tener acceso a ellas de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="89d74-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="89d74-151">En los siguientes ejemplos se muestra la forma de enviar un mensaje con la API Web.</span><span class="sxs-lookup"><span data-stu-id="89d74-151">The following examples show how to send a message using the Web API.</span></span>

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
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="89d74-152">Incorporación de un archivo adjunto</span><span class="sxs-lookup"><span data-stu-id="89d74-152">How to: Add an attachment</span></span>
<span data-ttu-id="89d74-153">Es posible agregar datos adjuntos a un mensaje llamando al método **AddAttachment** y especificando mínimamente el nombre de archivo y el contenido codificado en Base64 que desea adjuntar.</span><span class="sxs-lookup"><span data-stu-id="89d74-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="89d74-154">Puede incluir múltiples datos adjuntos mediante la llamada a este método, que debe utilizar una vez por cada archivo que desee adjuntar, o utilizando el método **AddAttachments**.</span><span class="sxs-lookup"><span data-stu-id="89d74-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="89d74-155">El siguiente ejemplo demuestra la incorporación de datos adjuntos a un mensaje:</span><span class="sxs-lookup"><span data-stu-id="89d74-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="89d74-156">Uso de la configuración de correo para habilitar pies de página, seguimiento y análisis</span><span class="sxs-lookup"><span data-stu-id="89d74-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="89d74-157">SendGrid proporciona funciones de correo electrónico adicionales mediante el uso de configuraciones de correo y de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="89d74-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="89d74-158">Todas estas configuraciones se pueden agregar a un mensaje de correo electrónico para habilitar funciones específicas, como el seguimiento por clics, Google Analytics, el seguimiento de suscripciones, etc.</span><span class="sxs-lookup"><span data-stu-id="89d74-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="89d74-159">Para obtener una lista completa de las aplicaciones, consulte la [documentación de la configuración][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="89d74-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="89d74-160">Es posible incluir aplicaciones en los mensajes de correo de **SendGrid** con métodos implementados como parte de la clase **SendGridMessage**.</span><span class="sxs-lookup"><span data-stu-id="89d74-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="89d74-161">Los siguientes ejemplos demuestran el uso de los filtros de pie de página y seguimiento por clics:</span><span class="sxs-lookup"><span data-stu-id="89d74-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="89d74-162">Los siguientes ejemplos demuestran el uso de los filtros de pie de página y seguimiento por clics:</span><span class="sxs-lookup"><span data-stu-id="89d74-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="89d74-163">Configuración de pie de página</span><span class="sxs-lookup"><span data-stu-id="89d74-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="89d74-164">Seguimiento por clics</span><span class="sxs-lookup"><span data-stu-id="89d74-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="89d74-165">Uso de servicios adicionales de SendGrid</span><span class="sxs-lookup"><span data-stu-id="89d74-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="89d74-166">SendGrid ofrece varias API y webhooks que puede usar para aprovechar la funcionalidad adicional dentro de la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="89d74-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="89d74-167">Para más detalles, consulte la [referencia de la API de SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="89d74-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="89d74-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89d74-168">Next steps</span></span>
<span data-ttu-id="89d74-169">Ahora que conoce los fundamentos del servicio de correo electrónico SendGrid, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="89d74-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="89d74-170">Repositorio de bibliotecas de C#\# de SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="89d74-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="89d74-171">Documentación sobre la API de SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="89d74-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
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

<span data-ttu-id="89d74-172">[servicio de correo electrónico basado en la nube]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="89d74-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="89d74-173">[entrega de correo electrónico transaccional]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="89d74-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

