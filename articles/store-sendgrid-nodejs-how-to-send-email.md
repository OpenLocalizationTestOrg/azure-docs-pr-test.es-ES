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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Cómo tooSend SendGrid de uso de correo electrónico de Node.js
Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure. ejemplos de Hola se escriben con hello API Node.js. Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, **agregar datos adjuntos**, **mediante filtros**y **actualizar propiedades**. Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos](#next-steps) sección.

## <a name="what-is-hello-sendgrid-email-service"></a>¿Qué es hello SendGrid servicio de correo electrónico?
SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada. Entre los escenarios de uso de SendGrid comunes se incluyen:

* Enviar automáticamente confirmaciones toocustomers
* Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes
* Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.
* Generar informes toohelp identificar tendencias
* Reenvío de consultas de los clientes
* Envío de notificaciones de correo electrónico desde su aplicación

Para obtener más información, consulte [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Creación de una cuenta de SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Hacer referencia a Hola módulo Node.js de SendGrid
módulo de SendGrid Hola para Node.js puede instalarse a través del Administrador de paquetes de nodo de hello (npm) mediante el uso de hello siguiente comando:

    npm install sendgrid

Después de la instalación, puede requerir módulo hello en la aplicación mediante el uso de hello siguiente código:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

módulo de SendGrid Hola exporta hello **SendGrid** y **correo electrónico** funciones.
**SendGrid** es responsable del envío de correo electrónico a través de la API web, mientras que **Email** encapsula un mensaje de correo electrónico.

## <a name="how-to-create-an-email"></a>Creación de un correo electrónico
Crear un mensaje de correo electrónico con hello SendGrid módulo implica crear primero un mensaje de correo electrónico utilizando la función de correo electrónico de hello y, a continuación, enviarla con hello SendGrid función. Hola te mostramos un ejemplo de cómo crear un nuevo mensaje mediante la función de correo electrónico de hello:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

También puede especificar un mensaje HTML para clientes que admiten estableciendo la propiedad de hello html. Por ejemplo:

    html: This is a sample <b>HTML<b> email message.

Establecer ambas propiedades de texto y el código html de hello proporciona estable reserva para contenido de texto para los clientes que no son compatibles con los mensajes de HTML.

Para obtener más información sobre todas las propiedades admitidas por hello función de correo electrónico, consulte [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Envío de un correo electrónico
Después de crear un mensaje de correo electrónico con hello función de correo electrónico, puede enviar mediante hello Web API proporcionada por SendGrid. 

### <a name="web-api"></a>API Web
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Mientras que Hola por encima de los ejemplos muestran pasar en una función de devolución de llamada y de objeto de correo electrónico, puede invocar directamente función de envío de hello especificando directamente las propiedades de correo electrónico. Por ejemplo:  
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

## <a name="how-to-add-an-attachment"></a>Adición de un correo electrónico
Pueden agregarse a los datos adjuntos tooa mensaje mediante la especificación de nombres de archivo de Hola y las rutas en hello **archivos** propiedad. Hola de ejemplo siguiente se muestra cómo enviar datos adjuntos:

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
> Cuando se usa hello **archivos** propiedad, el archivo hello debe ser accesible a través de [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Si el archivo hello desea tooattach se hospeda en el almacenamiento de Azure, como se muestra en un contenedor de blobs, primero debe copiar el almacenamiento de información de hello archivo toolocal o tooan unidad de Azure antes de que se pueden enviar como datos adjuntos con hello **archivos** propiedad.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Cómo: usar filtros tooEnable pies de página y el seguimiento
SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de filtros. Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente. Si desea obtener una lista completa de los filtros, consulte [Filter Settings][Filter Settings].

Los filtros pueden ser mensajes tooa aplicada mediante el uso de hello **filtros** propiedad.
Cada filtro se especifica mediante un hash que contiene la configuración específica del filtro.
Hello en los ejemplos siguientes muestran el pie de página de Hola y haga clic en filtros de seguimiento:

### <a name="footer"></a>Pie de página
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

### <a name="click-tracking"></a>Seguimiento por clics
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

## <a name="how-to-update-email-properties"></a>Actualización de las propiedades del correo electrónico
Algunas propiedades de correo electrónico se pueden sobrescribir con  **establecer*propiedad*** o estar anexados mediante  **agregar*propiedad***. Por ejemplo, puede agregar destinatarios adicionales mediante

    email.addTo('jeff@contoso.com');

o configurar un filtro mediante

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Para obtener más información, consulte [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Uso de servicios adicionales de SendGrid
SendGrid ofrece API basadas en web que puede usar la funcionalidad adicional de SendGrid de tooleverage desde la aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.

* Repositorio de módulos de SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]
* Documentación sobre la API de SendGrid: <https://sendgrid.com/docs>
* Oferta especial de SendGrid para clientes de Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[servicio de correo electrónico basado en la nube]: https://sendgrid.com/email-solutions
[entrega de correo electrónico transaccional]: https://sendgrid.com/transactional-email
