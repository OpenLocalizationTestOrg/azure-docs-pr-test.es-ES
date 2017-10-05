---
title: "Configuración de notificaciones y plantillas de correo electrónico en Azure API Management | Microsoft Docs"
description: "Obtenga información acerca de cómo configurar notificaciones y plantillas de correo electrónico en Administración de API de Azure."
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="c276a-103">Configuración de notificaciones y plantillas de correo electrónico en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="c276a-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="c276a-104">Administración de API ofrece la posibilidad de configurar notificaciones de eventos específicos, así como plantillas de correo electrónico que se usan para comunicarse con los administradores y desarrolladores de una instancia de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="c276a-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="c276a-105">Este tema muestra cómo configurar notificaciones de los eventos disponibles y ofrece información general sobre la configuración de plantillas de correo electrónico que se usan para estos eventos.</span><span class="sxs-lookup"><span data-stu-id="c276a-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="c276a-106"><a name="publisher-notifications"> </a>Configuración de notificaciones del publicador</span><span class="sxs-lookup"><span data-stu-id="c276a-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="c276a-107">Para configurar las notificaciones, haga clic en **Portal para editores** en Azure Portal en su servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="c276a-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="c276a-108">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="c276a-108">This takes you to the API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="c276a-110">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c276a-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="c276a-111">Haga clic en **Notificaciones** en el menú **API Management** de la izquierda para ver las notificaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="c276a-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Notificaciones del publicador][api-management-publisher-notifications]

<span data-ttu-id="c276a-113">Se puede configurar la siguiente lista de eventos para notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c276a-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="c276a-114">**Solicitudes de suscripción (se requiere aprobación)** : los destinatarios y usuarios de correo electrónico especificados recibirán notificaciones por correo electrónico sobre solicitudes de suscripción de productos de API que requieran aprobación.</span><span class="sxs-lookup"><span data-stu-id="c276a-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="c276a-115">**Nuevas suscripciones** : los destinatarios y usuarios de correo electrónico especificados recibirán notificaciones por correo electrónico sobre nuevas suscripciones de productos de API.</span><span class="sxs-lookup"><span data-stu-id="c276a-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="c276a-116">**Solicitudes de la galería de aplicaciones** : los destinatarios y usuarios de correo electrónico especificados recibirán notificaciones por correo electrónico cuando se envíen nuevas aplicaciones a la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c276a-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="c276a-117">**CCO** : los destinatarios y usuarios de correo electrónico especificados recibirán copias carbón ocultas de todos los correos electrónicos enviados a los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="c276a-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="c276a-118">**Nuevo problema o comentario** : los destinatarios y usuarios de correo electrónico especificados recibirán notificaciones por correo electrónico cuando se envíe un nuevo problema o comentario en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="c276a-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="c276a-119">**Cerrar mensaje de cuenta** : los destinatarios y usuarios de correo electrónico especificados recibirán notificaciones por correo electrónico cuando se cierre una cuenta.</span><span class="sxs-lookup"><span data-stu-id="c276a-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="c276a-120">**Aproximación al límite de cuota de suscripción** : los siguientes destinatarios y usuarios de correo electrónico recibirán notificaciones por correo electrónico cuando el uso de la suscripción se acerque a la cuota de uso.</span><span class="sxs-lookup"><span data-stu-id="c276a-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="c276a-121">En cada evento, se pueden especificar destinatarios con el cuadro de texto de dirección de correo electrónico o seleccionar usuarios de una lista.</span><span class="sxs-lookup"><span data-stu-id="c276a-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="c276a-122">Para especificar las direcciones de correo electrónico a las que se van a enviar notificaciones, especifíquelas en el cuadro de texto de dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c276a-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="c276a-123">Si tiene varias direcciones de correo electrónico, sepárelas con comas.</span><span class="sxs-lookup"><span data-stu-id="c276a-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="c276a-125">Para especificar los usuarios a los que se va a notificar, haga clic en **Agregar destinatario**, active la casilla situada junto a los usuarios a los que se va a notificar y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c276a-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="c276a-126">En la lista solo aparecen los administradores.</span><span class="sxs-lookup"><span data-stu-id="c276a-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="c276a-127">Después de configurar los destinatarios de las notificaciones, haga clic en **Guardar** para aplicar los destinatarios de notificación actualizados.</span><span class="sxs-lookup"><span data-stu-id="c276a-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="c276a-128">Si hay cambios sin guardar y sale de la pestaña **Notificaciones del publicador** , el portal del publicador le avisará.</span><span class="sxs-lookup"><span data-stu-id="c276a-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="c276a-129"><a name="email-templates"> </a>Configuración de plantillas de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="c276a-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="c276a-130">Administración de API proporciona plantillas de correo electrónico para los mensajes de correo electrónico que se envían durante la administración y el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="c276a-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="c276a-131">Se incluyen las siguientes plantillas de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c276a-131">The following email templates are provided.</span></span>

* <span data-ttu-id="c276a-132">Envío de la galería de aplicaciones aprobado</span><span class="sxs-lookup"><span data-stu-id="c276a-132">Application gallery submission approved</span></span>
* <span data-ttu-id="c276a-133">Carta de despedida del desarrollador</span><span class="sxs-lookup"><span data-stu-id="c276a-133">Developer farewell letter</span></span>
* <span data-ttu-id="c276a-134">Notificación de aproximación del límite de cuota del desarrollador</span><span class="sxs-lookup"><span data-stu-id="c276a-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="c276a-135">Invitación a un usuario</span><span class="sxs-lookup"><span data-stu-id="c276a-135">Invite user</span></span>
* <span data-ttu-id="c276a-136">Nuevo comentario agregado a un problema</span><span class="sxs-lookup"><span data-stu-id="c276a-136">New comment added to an issue</span></span>
* <span data-ttu-id="c276a-137">Nuevo problema recibido</span><span class="sxs-lookup"><span data-stu-id="c276a-137">New issue received</span></span>
* <span data-ttu-id="c276a-138">Nueva suscripción activada</span><span class="sxs-lookup"><span data-stu-id="c276a-138">New subscription activated</span></span>
* <span data-ttu-id="c276a-139">Confirmación de suscripción renovada</span><span class="sxs-lookup"><span data-stu-id="c276a-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="c276a-140">Rechazo de la solicitud de suscripción</span><span class="sxs-lookup"><span data-stu-id="c276a-140">Subscription request declines</span></span>
* <span data-ttu-id="c276a-141">Solicitud de suscripción recibida</span><span class="sxs-lookup"><span data-stu-id="c276a-141">Subscription request received</span></span>

<span data-ttu-id="c276a-142">Estas plantillas se pueden modificar tal como se desee.</span><span class="sxs-lookup"><span data-stu-id="c276a-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="c276a-143">Para ver y configurar las plantillas de correo electrónico de la instancia de API Management, haga clic en **Notificaciones** en el menú **API Management** de la izquierda y seleccione la pestaña **Plantillas de correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="c276a-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="c276a-145">Para ver o modificar una plantilla específica, selecciónela en de la lista desplegable **Plantillas** .</span><span class="sxs-lookup"><span data-stu-id="c276a-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="c276a-147">Cada plantilla de correo electrónico tiene un asunto en texto sin formato y una definición del cuerpo en formato HTML.</span><span class="sxs-lookup"><span data-stu-id="c276a-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="c276a-148">Cada elemento se puede personalizar según se desee.</span><span class="sxs-lookup"><span data-stu-id="c276a-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="c276a-150">La lista **Parámetros** contiene una lista de parámetros que, al insertarlos en el asunto o en el cuerpo, se reemplazarán por el valor designado cuando se envíe el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c276a-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="c276a-151">Para insertar un parámetro, sitúe el cursor en donde desee que vaya el parámetro y haga clic en la flecha a la izquierda del nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="c276a-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="c276a-152">Haga clic en **Vista previa** o en **Enviar una prueba** para ver el aspecto que tendrá el correo electrónico o para enviar un correo electrónico de prueba.</span><span class="sxs-lookup"><span data-stu-id="c276a-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="c276a-153">Los parámetros no se reemplazan por valores reales al obtener la vista previa o enviar una prueba.</span><span class="sxs-lookup"><span data-stu-id="c276a-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="c276a-154">Para guardar los cambios efectuados en la plantilla de correo electrónico, haga clic en **Guardar** o, si desea cancelarlos, haga clic en **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="c276a-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
