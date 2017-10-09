---
title: "aaaHow toouse Hola servicio de correo electrónico de SendGrid (Node.js) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico de SendGrid hello en Azure. Escrito mediante Hola API Node.js de ejemplos de código."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="3885f-104">Cómo tooSend SendGrid de uso de correo electrónico de Node.js</span><span class="sxs-lookup"><span data-stu-id="3885f-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="3885f-105">Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="3885f-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="3885f-106">ejemplos de Hola se escriben con hello API Node.js.</span><span class="sxs-lookup"><span data-stu-id="3885f-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="3885f-107">Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, **agregar datos adjuntos**, **mediante filtros**y **actualizar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3885f-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="3885f-108">Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="3885f-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="3885f-109">¿Qué es hello SendGrid servicio de correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="3885f-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="3885f-110">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="3885f-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="3885f-111">Entre los escenarios de uso de SendGrid comunes se incluyen:</span><span class="sxs-lookup"><span data-stu-id="3885f-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="3885f-112">Enviar automáticamente confirmaciones toocustomers</span><span class="sxs-lookup"><span data-stu-id="3885f-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="3885f-113">Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes</span><span class="sxs-lookup"><span data-stu-id="3885f-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="3885f-114">Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="3885f-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="3885f-115">Generar informes toohelp identificar tendencias</span><span class="sxs-lookup"><span data-stu-id="3885f-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="3885f-116">Reenvío de consultas de los clientes</span><span class="sxs-lookup"><span data-stu-id="3885f-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="3885f-117">Envío de notificaciones de correo electrónico desde su aplicación</span><span class="sxs-lookup"><span data-stu-id="3885f-117">Email notifications from your application</span></span>

<span data-ttu-id="3885f-118">Para obtener más información, consulte [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="3885f-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="3885f-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="3885f-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="3885f-120">Hacer referencia a Hola módulo Node.js de SendGrid</span><span class="sxs-lookup"><span data-stu-id="3885f-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="3885f-121">módulo de SendGrid Hola para Node.js puede instalarse a través del Administrador de paquetes de nodo de hello (npm) mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3885f-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="3885f-122">Después de la instalación, puede requerir módulo hello en la aplicación mediante el uso de hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="3885f-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="3885f-123">módulo de SendGrid Hola exporta hello **SendGrid** y **correo electrónico** funciones.</span><span class="sxs-lookup"><span data-stu-id="3885f-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="3885f-124">**SendGrid** es responsable del envío de correo electrónico a través de la API web, mientras que **Email** encapsula un mensaje de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="3885f-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="3885f-125">Creación de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="3885f-125">How to: Create an Email</span></span>
<span data-ttu-id="3885f-126">Crear un mensaje de correo electrónico con hello SendGrid módulo implica crear primero un mensaje de correo electrónico utilizando la función de correo electrónico de hello y, a continuación, enviarla con hello SendGrid función.</span><span class="sxs-lookup"><span data-stu-id="3885f-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="3885f-127">Hola te mostramos un ejemplo de cómo crear un nuevo mensaje mediante la función de correo electrónico de hello:</span><span class="sxs-lookup"><span data-stu-id="3885f-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="3885f-128">También puede especificar un mensaje HTML para clientes que admiten estableciendo la propiedad de hello html.</span><span class="sxs-lookup"><span data-stu-id="3885f-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="3885f-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3885f-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="3885f-130">Establecer ambas propiedades de texto y el código html de hello proporciona estable reserva para contenido de texto para los clientes que no son compatibles con los mensajes de HTML.</span><span class="sxs-lookup"><span data-stu-id="3885f-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="3885f-131">Para obtener más información sobre todas las propiedades admitidas por hello función de correo electrónico, consulte [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="3885f-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="3885f-132">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="3885f-132">How to: Send an Email</span></span>
<span data-ttu-id="3885f-133">Después de crear un mensaje de correo electrónico con hello función de correo electrónico, puede enviar mediante hello Web API proporcionada por SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3885f-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="3885f-134">API Web</span><span class="sxs-lookup"><span data-stu-id="3885f-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="3885f-135">Mientras que Hola por encima de los ejemplos muestran pasar en una función de devolución de llamada y de objeto de correo electrónico, puede invocar directamente función de envío de hello especificando directamente las propiedades de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="3885f-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="3885f-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3885f-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="3885f-137">Adición de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="3885f-137">How to: Add an Attachment</span></span>
<span data-ttu-id="3885f-138">Pueden agregarse a los datos adjuntos tooa mensaje mediante la especificación de nombres de archivo de Hola y las rutas en hello **archivos** propiedad.</span><span class="sxs-lookup"><span data-stu-id="3885f-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="3885f-139">Hola de ejemplo siguiente se muestra cómo enviar datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="3885f-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="3885f-140">Cuando se usa hello **archivos** propiedad, el archivo hello debe ser accesible a través de [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="3885f-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="3885f-141">Si el archivo hello desea tooattach se hospeda en el almacenamiento de Azure, como se muestra en un contenedor de blobs, primero debe copiar el almacenamiento de información de hello archivo toolocal o tooan unidad de Azure antes de que se pueden enviar como datos adjuntos con hello **archivos** propiedad.</span><span class="sxs-lookup"><span data-stu-id="3885f-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="3885f-142">Cómo: usar filtros tooEnable pies de página y el seguimiento</span><span class="sxs-lookup"><span data-stu-id="3885f-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="3885f-143">SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de filtros.</span><span class="sxs-lookup"><span data-stu-id="3885f-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="3885f-144">Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3885f-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="3885f-145">Si desea obtener una lista completa de los filtros, consulte [Filter Settings][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="3885f-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="3885f-146">Los filtros pueden ser mensajes tooa aplicada mediante el uso de hello **filtros** propiedad.</span><span class="sxs-lookup"><span data-stu-id="3885f-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="3885f-147">Cada filtro se especifica mediante un hash que contiene la configuración específica del filtro.</span><span class="sxs-lookup"><span data-stu-id="3885f-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="3885f-148">Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="3885f-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="3885f-149">Pie de página</span><span class="sxs-lookup"><span data-stu-id="3885f-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="3885f-150">Seguimiento por clics</span><span class="sxs-lookup"><span data-stu-id="3885f-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="3885f-151">Actualización de las propiedades del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="3885f-151">How to: Update Email Properties</span></span>
<span data-ttu-id="3885f-152">Algunas propiedades de correo electrónico se pueden sobrescribir con  **establecer*propiedad*** o estar anexados mediante  **agregar*propiedad***.</span><span class="sxs-lookup"><span data-stu-id="3885f-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="3885f-153">Por ejemplo, puede agregar destinatarios adicionales mediante</span><span class="sxs-lookup"><span data-stu-id="3885f-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="3885f-154">o configurar un filtro mediante</span><span class="sxs-lookup"><span data-stu-id="3885f-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="3885f-155">Para obtener más información, consulte [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="3885f-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="3885f-156">Uso de servicios adicionales de SendGrid</span><span class="sxs-lookup"><span data-stu-id="3885f-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="3885f-157">SendGrid ofrece API basadas en web que puede usar la funcionalidad adicional de SendGrid de tooleverage desde la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="3885f-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="3885f-158">Para obtener información detallada, vea hello [documentación de la API de SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="3885f-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3885f-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3885f-159">Next Steps</span></span>
<span data-ttu-id="3885f-160">Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="3885f-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="3885f-161">Repositorio de módulos de SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="3885f-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="3885f-162">Documentación sobre la API de SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="3885f-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="3885f-163">Oferta especial de SendGrid para clientes de Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="3885f-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[servicio de correo electrónico basado en la nube]: https://sendgrid.com/email-solutions
[entrega de correo electrónico transaccional]: https://sendgrid.com/transactional-email
