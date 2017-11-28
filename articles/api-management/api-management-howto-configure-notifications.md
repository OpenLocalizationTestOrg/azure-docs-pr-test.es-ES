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
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="340c4-103">¿Cómo tooconfigure notificaciones y enviar por correo electrónico plantillas en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="340c4-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="340c4-104">Administración de API permite hello tooconfigure notificaciones de eventos específicos y las plantillas de correo electrónico de hello tooconfigure que son utilizado toocommunicate con los administradores de Hola y desarrolladores de una instancia de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="340c4-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="340c4-105">Este tema muestra cómo tooconfigure notificaciones para Hola eventos disponibles y proporciona una visión general de configuración de plantillas de correo electrónico de hello usa estos eventos.</span><span class="sxs-lookup"><span data-stu-id="340c4-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="340c4-106"><a name="publisher-notifications"></a>Configuración de notificaciones del publicador</span><span class="sxs-lookup"><span data-stu-id="340c4-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="340c4-107">notificaciones de tooconfigure, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="340c4-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="340c4-108">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="340c4-108">This takes you toohello API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="340c4-110">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="340c4-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="340c4-111">Haga clic en **notificaciones** de hello **administración de API** menú Hola deja tooview notificaciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Notificaciones del publicador][api-management-publisher-notifications]

<span data-ttu-id="340c4-113">Hello siguiente lista de eventos se puede configurar para las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="340c4-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="340c4-114">**Las solicitudes de suscripción (lo que requiere aprobación)** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico acerca de las solicitudes de suscripción para productos de API que requieren aprobación.</span><span class="sxs-lookup"><span data-stu-id="340c4-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="340c4-115">**Las nuevas suscripciones** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico sobre nuevas suscripciones de producto de API.</span><span class="sxs-lookup"><span data-stu-id="340c4-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="340c4-116">**Las solicitudes de la Galería de aplicaciones** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico nuevas aplicaciones una vez enviado toohello Galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="340c4-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="340c4-117">**CCO** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán copias ocultas de correo electrónico de toodevelopers de todos los correos electrónicos enviados.</span><span class="sxs-lookup"><span data-stu-id="340c4-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="340c4-118">**Problema nuevo o tu comentario** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico cuando un nuevo asunto o comentario se envía en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="340c4-119">**Mensaje de cerrar cuenta** : Hola destinatarios de correo electrónico especificado y los usuarios recibirán notificaciones de correo electrónico cuando se cierra una cuenta.</span><span class="sxs-lookup"><span data-stu-id="340c4-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="340c4-120">**Límite de cuota de suscripción con** : Hola después de destinatarios de correo electrónico y los usuarios recibirán notificaciones de correo electrónico al uso de la suscripción obtiene cuota toousage cerrar.</span><span class="sxs-lookup"><span data-stu-id="340c4-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="340c4-121">Para cada evento, puede especificar a los destinatarios de correo electrónico mediante el cuadro de texto de dirección de correo electrónico de Hola o puede seleccionar los usuarios de una lista.</span><span class="sxs-lookup"><span data-stu-id="340c4-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="340c4-122">toospecify hello toobe de direcciones de correo electrónico una notificación, escríbalas en el cuadro de texto de dirección de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="340c4-123">Si tiene varias direcciones de correo electrónico, sepárelas con comas.</span><span class="sxs-lookup"><span data-stu-id="340c4-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="340c4-125">toospecify Hola usuarios toobe una notificación, haga clic en **Agregar destinatario**, Hola de casilla al lado de hello usuarios toobe una notificación y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="340c4-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="340c4-126">Solo los administradores se muestran en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="340c4-127">Después de configurar los destinatarios de notificaciones de hello, haga clic en **guardar** tooapply Hola actualiza destinatarios de notificación.</span><span class="sxs-lookup"><span data-stu-id="340c4-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="340c4-128">Si sale de hello **Publisher notificaciones** portal para desarrolladores de pestaña Hola le avisa si hay cambios no guardados.</span><span class="sxs-lookup"><span data-stu-id="340c4-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="340c4-129"><a name="email-templates"></a>Configuración de plantillas de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="340c4-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="340c4-130">Administración de API proporciona plantillas de correo electrónico para hello mensajes de correo electrónico que se envían en curso de Hola de administrar y usar servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="340c4-131">se proporciona Hola siguiendo las plantillas de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="340c4-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="340c4-132">Envío de la galería de aplicaciones aprobado</span><span class="sxs-lookup"><span data-stu-id="340c4-132">Application gallery submission approved</span></span>
* <span data-ttu-id="340c4-133">Carta de despedida del desarrollador</span><span class="sxs-lookup"><span data-stu-id="340c4-133">Developer farewell letter</span></span>
* <span data-ttu-id="340c4-134">Notificación de aproximación del límite de cuota del desarrollador</span><span class="sxs-lookup"><span data-stu-id="340c4-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="340c4-135">Invitación a un usuario</span><span class="sxs-lookup"><span data-stu-id="340c4-135">Invite user</span></span>
* <span data-ttu-id="340c4-136">Nuevo comentario agregado tooan problema</span><span class="sxs-lookup"><span data-stu-id="340c4-136">New comment added tooan issue</span></span>
* <span data-ttu-id="340c4-137">Nuevo problema recibido</span><span class="sxs-lookup"><span data-stu-id="340c4-137">New issue received</span></span>
* <span data-ttu-id="340c4-138">Nueva suscripción activada</span><span class="sxs-lookup"><span data-stu-id="340c4-138">New subscription activated</span></span>
* <span data-ttu-id="340c4-139">Confirmación de suscripción renovada</span><span class="sxs-lookup"><span data-stu-id="340c4-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="340c4-140">Rechazo de la solicitud de suscripción</span><span class="sxs-lookup"><span data-stu-id="340c4-140">Subscription request declines</span></span>
* <span data-ttu-id="340c4-141">Solicitud de suscripción recibida</span><span class="sxs-lookup"><span data-stu-id="340c4-141">Subscription request received</span></span>

<span data-ttu-id="340c4-142">Estas plantillas se pueden modificar tal como se desee.</span><span class="sxs-lookup"><span data-stu-id="340c4-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="340c4-143">tooview y configurar plantillas de correo electrónico de hello para la instancia de la administración de API, haga clic en **notificaciones** de hello **administración de API** menú Hola izquierda y seleccione hello **plantillas de correo electrónico**  ficha.</span><span class="sxs-lookup"><span data-stu-id="340c4-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="340c4-145">tooview o modificar una plantilla específica, selecciónela en hello **plantillas** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="340c4-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="340c4-147">Cada plantilla de correo electrónico tiene un asunto en texto sin formato y una definición del cuerpo en formato HTML.</span><span class="sxs-lookup"><span data-stu-id="340c4-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="340c4-148">Cada elemento se puede personalizar según se desee.</span><span class="sxs-lookup"><span data-stu-id="340c4-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="340c4-150">Hola **parámetros** lista contiene una lista de parámetros, que cuando se inserta Hola asunto ni un cuerpo, será el valor de hello reemplazado designado cuando se envía correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="340c4-151">tooinsert un parámetro, coloque cursor de Hola donde desea Hola parámetro toogo y haga clic en hello flecha toohello a la izquierda del nombre de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="340c4-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="340c4-152">Haga clic en **vista previa** o **enviar una prueba** toosee cómo correo electrónico Hola se buscar o enviar un correo electrónico de prueba.</span><span class="sxs-lookup"><span data-stu-id="340c4-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="340c4-153">parámetros de Hello no se reemplazan por valores reales al obtener una vista previa o enviar una prueba.</span><span class="sxs-lookup"><span data-stu-id="340c4-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="340c4-154">plantilla de correo electrónico de toohello de toosave Hola cambios, haga clic en **guardar**, o haga clic en cambios de hello toocancel **cancelar**.</span><span class="sxs-lookup"><span data-stu-id="340c4-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

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
