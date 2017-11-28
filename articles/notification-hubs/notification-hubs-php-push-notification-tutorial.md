---
title: aaaHow toouse centros de notificaciones con PHP
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Azure de un back-end PHP."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="66189-103">¿Cómo toouse centros de notificaciones de PHP</span><span class="sxs-lookup"><span data-stu-id="66189-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="66189-104">Puede tener acceso a todas las características de los centros de notificaciones de un back-end de Java, PHP y Ruby mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="66189-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="66189-105">En este tema le mostraremos cómo:</span><span class="sxs-lookup"><span data-stu-id="66189-105">In this topic we show how to:</span></span>

* <span data-ttu-id="66189-106">Crear un cliente REST para las características de Centros de notificaciones en PHP;</span><span class="sxs-lookup"><span data-stu-id="66189-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="66189-107">Siga hello [tutorial introductorio Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) para su plataforma móvil de elección, implementar parte de back-end de hello en PHP.</span><span class="sxs-lookup"><span data-stu-id="66189-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="66189-108">Interfaz del cliente</span><span class="sxs-lookup"><span data-stu-id="66189-108">Client interface</span></span>
<span data-ttu-id="66189-109">interfaz de cliente principal de Hello puede proporcionar Hola mismos métodos que están disponibles en hello [.NET SDK de los centros de notificación](http://msdn.microsoft.com/library/jj933431.aspx), esto le permitirá toodirectly traducir todos los tutoriales de Hola y ejemplos, está disponibles en este sitio, y aportados por la Comunidad de hello en hello internet.</span><span class="sxs-lookup"><span data-stu-id="66189-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="66189-110">Puede encontrar todo el código de hello disponible en hello [ejemplo de contenedor de REST de PHP].</span><span class="sxs-lookup"><span data-stu-id="66189-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="66189-111">Por ejemplo, toocreate un cliente:</span><span class="sxs-lookup"><span data-stu-id="66189-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="66189-112">toosend una notificación nativa de iOS:</span><span class="sxs-lookup"><span data-stu-id="66189-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="66189-113">Implementación</span><span class="sxs-lookup"><span data-stu-id="66189-113">Implementation</span></span>
<span data-ttu-id="66189-114">Si aún no lo hizo, siga nuestro [tutorial introductorio Get] una copia de seguridad toohello última sección donde haya tooimplement Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="66189-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="66189-115">Además, si desea que se puede utilizar el código de hello de hello [ejemplo de contenedor de REST de PHP] e ir directamente a toohello [tutorial Hola completa](#complete-tutorial) sección.</span><span class="sxs-lookup"><span data-stu-id="66189-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="66189-116">Todos Hola tooimplement detalles que se encuentra en un contenedor REST completo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="66189-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="66189-117">En esta sección vamos a describir la implementación de PHP Hola de hello pasos principales necesarios tooaccess extremos REST de centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="66189-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="66189-118">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="66189-118">Parse hello connection string</span></span>
2. <span data-ttu-id="66189-119">Generar el token de autorización de Hola</span><span class="sxs-lookup"><span data-stu-id="66189-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="66189-120">Realizar llamadas de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="66189-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="66189-121">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="66189-121">Parse hello connection string</span></span>
<span data-ttu-id="66189-122">Aquí es Hola clase principal implementación Hola cliente, cuyo constructor que analiza la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="66189-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="66189-123">Creación del token de seguridad</span><span class="sxs-lookup"><span data-stu-id="66189-123">Create security token</span></span>
<span data-ttu-id="66189-124">detalles de Hola de creación de tokens de seguridad de hello [aquí](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="66189-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="66189-125">método siguiente Hello tiene toobe agregado toohello **NotificationHub** token de Hola de clase toocreate basado en URI de solicitud actual de Hola y las credenciales de hello extraídas de la cadena de conexión de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="66189-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="66189-126">Envío de una notificación</span><span class="sxs-lookup"><span data-stu-id="66189-126">Send a notification</span></span>
<span data-ttu-id="66189-127">En primer lugar, definamos una clase que representa una notificación.</span><span class="sxs-lookup"><span data-stu-id="66189-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="66189-128">Esta clase es un contenedor para un cuerpo de notificación nativa, o un conjunto de propiedades en el caso de una notificación de plantilla, y un conjunto de encabezados que contienen formato (plataforma o plantilla nativa) y propiedades específicas de la plataforma (como la propiedad de expiración de Apple y los encabezados WNS).</span><span class="sxs-lookup"><span data-stu-id="66189-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="66189-129">Consulte toohello [documentación de API de REST de bases de datos centrales de notificación](http://msdn.microsoft.com/library/dn495827.aspx) y Hola formatos de plataformas de notificación específico para todas las opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="66189-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="66189-130">Gracias a esta clase, ahora podemos escribir Hola envío métodos de notificación dentro de hello **NotificationHub** clase.</span><span class="sxs-lookup"><span data-stu-id="66189-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="66189-131">Hola por encima de los métodos de envío un punto de conexión de HTTP POST solicitud toohello /messages de su centro de notificaciones con cuerpo correcto de Hola y notificación de encabezados toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="66189-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="66189-132"><a name="complete-tutorial"></a>Tutorial de hello completa</span><span class="sxs-lookup"><span data-stu-id="66189-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="66189-133">Ahora puede completar el tutorial de introducción de hello mediante el envío de notificaciones de Hola de un back-end PHP.</span><span class="sxs-lookup"><span data-stu-id="66189-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="66189-134">Inicializar el cliente de los centros de notificaciones (sustituya el nombre de concentrador y la cadena de conexión de hello como se indica en hello [tutorial introductorio Get]):</span><span class="sxs-lookup"><span data-stu-id="66189-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="66189-135">A continuación, agregue código de envío de hello dependiendo de la plataforma de dispositivos móviles de destino.</span><span class="sxs-lookup"><span data-stu-id="66189-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="66189-136">Tienda Windows y Windows Phone 8.1 (no Silverlight)</span><span class="sxs-lookup"><span data-stu-id="66189-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="66189-137">iOS</span><span class="sxs-lookup"><span data-stu-id="66189-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="66189-138">Android</span><span class="sxs-lookup"><span data-stu-id="66189-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="66189-139">Silverlight para Windows Phone 8.0 y 8.1</span><span class="sxs-lookup"><span data-stu-id="66189-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="66189-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="66189-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="66189-141">La ejecución del código de PHP debe generar ahora una notificación que aparece en el dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="66189-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66189-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66189-142">Next Steps</span></span>
<span data-ttu-id="66189-143">En este tema se ha explicado cómo toocreate un Java simple de REST cliente centrales de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="66189-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="66189-144">Desde aquí puede:</span><span class="sxs-lookup"><span data-stu-id="66189-144">From here you can:</span></span>

* <span data-ttu-id="66189-145">Descargar Hola completa [ejemplo de contenedor de REST de PHP], que contiene todo el código de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="66189-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="66189-146">Seguir obteniendo información acerca de los centros de notificaciones etiquetado característica Hola [tutorial de noticias de última hora]</span><span class="sxs-lookup"><span data-stu-id="66189-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="66189-147">Obtenga información sobre la inserción de los usuarios de tooindividual de notificaciones en [tutorial de informar a los usuarios]</span><span class="sxs-lookup"><span data-stu-id="66189-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="66189-148">Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="66189-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[ejemplo de contenedor de REST de PHP]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial introductorio Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

