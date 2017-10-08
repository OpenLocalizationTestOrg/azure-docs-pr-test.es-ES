---
title: "notificaciones de aaaConfigure y enviar por correo electrónico plantillas en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure notificaciones y enviar por correo electrónico plantillas en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>¿Cómo tooconfigure notificaciones y enviar por correo electrónico plantillas en la administración de API de Azure
Administración de API permite hello tooconfigure notificaciones de eventos específicos y las plantillas de correo electrónico de hello tooconfigure que son utilizado toocommunicate con los administradores de Hola y desarrolladores de una instancia de la administración de API. Este tema muestra cómo tooconfigure notificaciones para Hola eventos disponibles y proporciona una visión general de configuración de plantillas de correo electrónico de hello usa estos eventos.

## <a name="publisher-notifications"></a>Configuración de notificaciones del publicador
notificaciones de tooconfigure, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

![Portal del publicador][api-management-management-console]

> [!NOTE] 
> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.

Haga clic en **notificaciones** de hello **administración de API** menú Hola deja tooview notificaciones disponibles Hola.

![Notificaciones del publicador][api-management-publisher-notifications]

Hello siguiente lista de eventos se puede configurar para las notificaciones.

* **Las solicitudes de suscripción (lo que requiere aprobación)** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico acerca de las solicitudes de suscripción para productos de API que requieren aprobación.
* **Las nuevas suscripciones** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico sobre nuevas suscripciones de producto de API.
* **Las solicitudes de la Galería de aplicaciones** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico nuevas aplicaciones una vez enviado toohello Galería de aplicaciones.
* **CCO** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán copias ocultas de correo electrónico de toodevelopers de todos los correos electrónicos enviados.
* **Problema nuevo o tu comentario** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico cuando un nuevo asunto o comentario se envía en el portal para desarrolladores de Hola.
* **Mensaje de cerrar cuenta** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico cuando se cierra una cuenta.
* **Límite de cuota de suscripción con** : Hola después de destinatarios de correo electrónico y los usuarios recibirán notificaciones de correo electrónico al uso de la suscripción obtiene cuota toousage cerrar.

Para cada evento, puede especificar a los destinatarios de correo electrónico mediante el cuadro de texto de dirección de correo electrónico de Hola o puede seleccionar los usuarios de una lista.

toospecify hello toobe de direcciones de correo electrónico una notificación, escríbalas en el cuadro de texto de dirección de correo electrónico de Hola. Si tiene varias direcciones de correo electrónico, sepárelas con comas.

![Notification recipients][api-management-email-addresses]

toospecify Hola usuarios toobe una notificación, haga clic en **Agregar destinatario**, Hola de casilla al lado de hello usuarios toobe una notificación y haga clic en **Aceptar**.

> [!NOTE] 
> Solo los administradores se muestran en la lista de Hola.


Después de configurar los destinatarios de notificaciones de hello, haga clic en **guardar** tooapply Hola actualiza destinatarios de notificación.

> [!NOTE] 
> Si sale de hello **Publisher notificaciones** portal para desarrolladores de pestaña Hola le avisa si hay cambios no guardados.


## <a name="email-templates"></a>Configuración de plantillas de correo electrónico
Administración de API proporciona plantillas de correo electrónico para hello mensajes de correo electrónico que se envían en curso de Hola de administrar y usar servicio de Hola. se proporciona Hola siguiendo las plantillas de correo electrónico.

* Envío de la galería de aplicaciones aprobado
* Carta de despedida del desarrollador
* Notificación de aproximación del límite de cuota del desarrollador
* Invitación a un usuario
* Nuevo comentario agregado tooan problema
* Nuevo problema recibido
* Nueva suscripción activada
* Confirmación de suscripción renovada
* Rechazo de la solicitud de suscripción
* Solicitud de suscripción recibida

Estas plantillas se pueden modificar tal como se desee.

tooview y configurar plantillas de correo electrónico de hello para la instancia de la administración de API, haga clic en **notificaciones** de hello **administración de API** menú Hola izquierda y seleccione hello **plantillas de correo electrónico**  ficha.

![Email templates][api-management-email-templates]

tooview o modificar una plantilla específica, selecciónela en hello **plantillas** lista desplegable.

![Email templates list][api-management-email-templates-list]

Cada plantilla de correo electrónico tiene un asunto en texto sin formato y una definición del cuerpo en formato HTML. Cada elemento se puede personalizar según se desee.

![Email template editor][api-management-email-template]

Hola **parámetros** lista contiene una lista de parámetros, que cuando se inserta Hola asunto ni un cuerpo, será el valor de hello reemplazado designado cuando se envía correo electrónico de Hola. tooinsert un parámetro, coloque cursor de Hola donde desea Hola parámetro toogo y haga clic en hello flecha toohello a la izquierda del nombre de parámetro de Hola.

Haga clic en **vista previa** o **enviar una prueba** toosee cómo correo electrónico Hola se buscar o enviar un correo electrónico de prueba.

> [!NOTE] 
> parámetros de Hello no se reemplazan por valores reales al obtener una vista previa o enviar una prueba.

plantilla de correo electrónico de toohello de toosave Hola cambios, haga clic en **guardar**, o haga clic en cambios de hello toocancel **cancelar**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
