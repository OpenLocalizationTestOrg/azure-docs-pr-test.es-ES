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
# <a name="how-toouse-notification-hubs-from-php"></a>¿Cómo toouse centros de notificaciones de PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Puede tener acceso a todas las características de los centros de notificaciones de un back-end de Java, PHP y Ruby mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx).

En este tema le mostraremos cómo:

* Crear un cliente REST para las características de Centros de notificaciones en PHP;
* Siga hello [tutorial introductorio Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) para su plataforma móvil de elección, implementar parte de back-end de hello en PHP.

## <a name="client-interface"></a>Interfaz del cliente
interfaz de cliente principal de Hello puede proporcionar Hola mismos métodos que están disponibles en hello [.NET SDK de los centros de notificación](http://msdn.microsoft.com/library/jj933431.aspx), esto le permitirá toodirectly traducir todos los tutoriales de Hola y ejemplos, está disponibles en este sitio, y aportados por la Comunidad de hello en hello internet.

Puede encontrar todo el código de hello disponible en hello [ejemplo de contenedor de REST de PHP].

Por ejemplo, toocreate un cliente:

    $hub = new NotificationHub("connection string", "hubname");    

toosend una notificación nativa de iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implementación
Si aún no lo hizo, siga nuestro [tutorial introductorio Get] una copia de seguridad toohello última sección donde haya tooimplement Hola back-end.
Además, si desea que se puede utilizar el código de hello de hello [ejemplo de contenedor de REST de PHP] e ir directamente a toohello [tutorial Hola completa](#complete-tutorial) sección.

Todos Hola tooimplement detalles que se encuentra en un contenedor REST completo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). En esta sección vamos a describir la implementación de PHP Hola de hello pasos principales necesarios tooaccess extremos REST de centros de notificaciones:

1. Analizar la cadena de conexión de Hola
2. Generar el token de autorización de Hola
3. Realizar llamadas de hello HTTP

### <a name="parse-hello-connection-string"></a>Analizar la cadena de conexión de Hola
Aquí es Hola clase principal implementación Hola cliente, cuyo constructor que analiza la cadena de conexión de hello:

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


### <a name="create-security-token"></a>Creación del token de seguridad
detalles de Hola de creación de tokens de seguridad de hello [aquí](http://msdn.microsoft.com/library/dn495627.aspx).
método siguiente Hello tiene toobe agregado toohello **NotificationHub** token de Hola de clase toocreate basado en URI de solicitud actual de Hola y las credenciales de hello extraídas de la cadena de conexión de Hola Hola.

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

### <a name="send-a-notification"></a>Envío de una notificación
En primer lugar, definamos una clase que representa una notificación.

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

Esta clase es un contenedor para un cuerpo de notificación nativa, o un conjunto de propiedades en el caso de una notificación de plantilla, y un conjunto de encabezados que contienen formato (plataforma o plantilla nativa) y propiedades específicas de la plataforma (como la propiedad de expiración de Apple y los encabezados WNS).

Consulte toohello [documentación de API de REST de bases de datos centrales de notificación](http://msdn.microsoft.com/library/dn495827.aspx) y Hola formatos de plataformas de notificación específico para todas las opciones disponibles de Hola.

Gracias a esta clase, ahora podemos escribir Hola envío métodos de notificación dentro de hello **NotificationHub** clase.

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

Hola por encima de los métodos de envío un punto de conexión de HTTP POST solicitud toohello /messages de su centro de notificaciones con cuerpo correcto de Hola y notificación de encabezados toosend Hola.

## <a name="complete-tutorial"></a>Tutorial de hello completa
Ahora puede completar el tutorial de introducción de hello mediante el envío de notificaciones de Hola de un back-end PHP.

Inicializar el cliente de los centros de notificaciones (sustituya el nombre de concentrador y la cadena de conexión de hello como se indica en hello [tutorial introductorio Get]):

    $hub = new NotificationHub("connection string", "hubname");    

A continuación, agregue código de envío de hello dependiendo de la plataforma de dispositivos móviles de destino.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Tienda Windows y Windows Phone 8.1 (no Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Silverlight para Windows Phone 8.0 y 8.1
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


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

La ejecución del código de PHP debe generar ahora una notificación que aparece en el dispositivo de destino.

## <a name="next-steps"></a>Pasos siguientes
En este tema se ha explicado cómo toocreate un Java simple de REST cliente centrales de notificaciones. Desde aquí puede:

* Descargar Hola completa [ejemplo de contenedor de REST de PHP], que contiene todo el código de hello anterior.
* Seguir obteniendo información acerca de los centros de notificaciones etiquetado característica Hola [tutorial de noticias de última hora]
* Obtenga información sobre la inserción de los usuarios de tooindividual de notificaciones en [tutorial de informar a los usuarios]

Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).

[ejemplo de contenedor de REST de PHP]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial introductorio Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

