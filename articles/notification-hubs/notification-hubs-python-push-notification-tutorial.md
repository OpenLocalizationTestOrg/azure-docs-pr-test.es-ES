---
title: aaaHow toouse centros de notificaciones con Python
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Azure de un back-end de Python."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>¿Cómo toouse centros de notificaciones de Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Puede tener acceso a todas las características de los centros de notificaciones de un Java/PHP y Python y Ruby back-end mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Esto es una implementación de referencia de ejemplo para implementar envía notificaciones de hello en Python y no es hello es compatible oficialmente SDK de Python de centro de notificaciones.
> 
> Este ejemplo está escrito con Python 3.4.
> 
> 

En este tema le mostraremos cómo:

* Cree un cliente REST para las características de los centros de notificaciones de Python.
* Enviar notificaciones mediante Hola Python interfaz toohello API de REST de concentrador de notificación. 
* Obtener un volcado de saludo de solicitud/respuesta HTTP REST propósito depuración educativos. 

Puede seguir hello [tutorial introductorio Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) para su plataforma móvil de elección, implementar parte de back-end de hello en Python.

> [!NOTE]
> ámbito de Hola de ejemplo de Hola es solamente las notificaciones de toosend limitado y todavía no hace ninguna administración del registro.
> 
> 

## <a name="client-interface"></a>Interfaz del cliente
interfaz de cliente principal de Hello puede proporcionar Hola mismos métodos que están disponibles en hello [.NET SDK de los centros de notificación](http://msdn.microsoft.com/library/jj933431.aspx). Esto le permitirá toodirectly traducir todos los tutoriales de Hola y ejemplos, está disponibles en este sitio y aportados por la Comunidad de hello en hello internet.

Puede encontrar todo el código de hello disponible en hello [ejemplo de contenedor de REST de Python].

Por ejemplo, toocreate un cliente:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

Introducción a toosend una ventana del sistema notificación:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Implementación
Si aún no lo hizo, siga nuestro [tutorial introductorio Get] una copia de seguridad toohello última sección donde haya tooimplement Hola back-end.

Todos Hola tooimplement detalles que se encuentra en un contenedor REST completo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). En esta sección se describen implementación de Python de Hola de hello pasos principales necesarios tooaccess extremos REST de centros de notificaciones y enviar notificaciones

1. Analizar la cadena de conexión de Hola
2. Generar el token de autorización de Hola
3. Enviar una notificación mediante la API REST de HTTP

### <a name="parse-hello-connection-string"></a>Analizar la cadena de conexión de Hola
Aquí es implementar el cliente de hello, cuyo constructor analiza la cadena de conexión de Hola de clase principal de hello:

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Creación del token de seguridad
detalles de Hola de creación de tokens de seguridad de hello [aquí](http://msdn.microsoft.com/library/dn495627.aspx).
Hello métodos siguientes tienen toobe agregado toohello **NotificationHub** token de Hola de clase toocreate basado en URI de solicitud actual de Hola y las credenciales de hello extraídas de la cadena de conexión de Hola Hola.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>Enviar una notificación mediante la API REST de HTTP
En primer lugar, definamos una clase que representa una notificación.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Esta clase es un contenedor para un cuerpo de notificación nativa, o un conjunto de propiedades en el caso de una notificación de plantilla, y un conjunto de encabezados que contienen formato (plataforma o plantilla nativa) y propiedades específicas de la plataforma (como la propiedad de expiración de Apple y los encabezados WNS).

Consulte toohello [documentación de API de REST de bases de datos centrales de notificación](http://msdn.microsoft.com/library/dn495827.aspx) y Hola formatos de plataformas de notificación específico para todas las opciones disponibles de Hola.

Ahora con esta clase, podemos escribir Hola envío métodos de notificación dentro de hello **NotificationHub** clase.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Hola por encima de los métodos de envío un punto de conexión de HTTP POST solicitud toohello /messages de su centro de notificaciones con cuerpo correcto de Hola y notificación de encabezados toosend Hola.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Usar depuración propiedad tooenable el registro detallado
Habilitar la propiedad de depuración al inicializar Hola centro de notificaciones escribirá información de registro detallada sobre Hola HTTP resultado de envío de solicitud y el volcado de respuesta, así como mensaje de notificación detallada. Recientemente hemos agregado esta propiedad llama [TestSend de bases de datos centrales de notificación propiedad](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) que devuelve información detallada sobre el resultado de enviar la notificación Hola. toouse lo - inicializar usando Hola siguientes:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

solicitud de envío de concentrador de notificación de Hello dirección URL HTTP se le anexan datos con una cadena de consulta de "prueba" como resultado. 

## <a name="complete-tutorial"></a>Tutorial de hello completa
Ahora puede completar el tutorial de introducción de hello mediante el envío de notificaciones de Hola de un back-end de Python.

Inicializar el cliente de los centros de notificaciones (sustituya el nombre de concentrador y la cadena de conexión de hello como se indica en hello [tutorial introductorio Get]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

A continuación, agregue código de envío de hello dependiendo de la plataforma de dispositivos móviles de destino. Este ejemplo también agrega tooenable de métodos de nivel superior enviar notificaciones basadas en la plataforma de hello p. ej. send_windows_notification para windows; send_apple_notification (para apple) etcetera. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Tienda Windows y Windows Phone 8.1 (no Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Silverlight para Windows Phone 8.0 y 8.1
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

La ejecución del código Python debe generar una notificación que se mostrará en el dispositivo de destino.

## <a name="examples"></a>Ejemplos:
### <a name="enabling-debug-property"></a>Habilitar la propiedad de depuración
Cuando se habilita la marca de depuración al inicializar hello NotificationHub verá detallada volcado de solicitud y respuesta HTTP, así como NotificationOutcome como siguiente Hola donde pueda entender qué encabezados HTTP se pasan en la solicitud de Hola y la ruta HTTP se recibió una respuesta de hello centro de notificaciones:![][1]

El resultado detallado del centro de notificaciones se mostrará, por ejemplo, 

* al mensaje Hola se envía correctamente toohello servicio de notificaciones Push. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Si hubiera se encontró ningún destino para las notificaciones de inserción, a continuación, es probable que se van toosee siguiente de Hola en respuesta de hello (que indica que había no se encontraron registros de notificación de hello toodeliver probablemente porque no tenían algunos registros de Hola no coinciden las etiquetas)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Difusión tooWindows de notificación de notificación del sistema
Tenga en cuenta los encabezados de Hola que obtengan envía cuando envía un cliente de tooWindows de notificación de sistema de difusión. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Enviar una notificación que especifica una etiqueta (o expresión de etiqueta)
Encabezado de HTTP de etiquetas de hello aviso que se agrega la solicitud de toohello HTTP (en el ejemplo de Hola a continuación, se envía Hola notificación solo tooregistrations con una carga de 'deportes')

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Enviar notificación que especifica varias etiquetas
Observe cómo el encabezado de HTTP de etiquetas de hello cambia cuando se envían varias etiquetas. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Notificación de plantilla
Observe que Hola formato HTTP de los cambios y cuerpo de la carga de Hola se envía como parte del cuerpo de la solicitud de hello HTTP:

**Cliente: plantilla registrada**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Servidor - envío de carga de Hola**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Pasos siguientes
En este tema se ha explicado cómo toocreate un simple de Python REST cliente centrales de notificaciones. Desde aquí puede:

* Descargar Hola completa [ejemplo de contenedor de REST de Python], que contiene todo el código de hello anterior.
* Seguir obteniendo información acerca de los centros de notificaciones etiquetado característica Hola [tutorial de noticias de última hora]
* Seguir obteniendo información acerca de la característica de plantillas de bases de datos centrales de notificación en hello [tutorial de noticias localizar]

<!-- URLs -->
[ejemplo de contenedor de REST de Python]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[tutorial introductorio Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[tutorial de noticias de última hora]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[tutorial de noticias localizar]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

