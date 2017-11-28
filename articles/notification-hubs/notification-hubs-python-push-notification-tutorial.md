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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="b962d-103">¿Cómo toouse centros de notificaciones de Python</span><span class="sxs-lookup"><span data-stu-id="b962d-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="b962d-104">Puede tener acceso a todas las características de los centros de notificaciones de un Java/PHP y Python y Ruby back-end mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="b962d-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b962d-105">Esto es una implementación de referencia de ejemplo para implementar envía notificaciones de hello en Python y no es hello es compatible oficialmente SDK de Python de centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="b962d-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="b962d-106">Este ejemplo está escrito con Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="b962d-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="b962d-107">En este tema le mostraremos cómo:</span><span class="sxs-lookup"><span data-stu-id="b962d-107">In this topic we show how to:</span></span>

* <span data-ttu-id="b962d-108">Cree un cliente REST para las características de los centros de notificaciones de Python.</span><span class="sxs-lookup"><span data-stu-id="b962d-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="b962d-109">Enviar notificaciones mediante Hola Python interfaz toohello API de REST de concentrador de notificación.</span><span class="sxs-lookup"><span data-stu-id="b962d-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="b962d-110">Obtener un volcado de saludo de solicitud/respuesta HTTP REST propósito depuración educativos.</span><span class="sxs-lookup"><span data-stu-id="b962d-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="b962d-111">Puede seguir hello [tutorial introductorio Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) para su plataforma móvil de elección, implementar parte de back-end de hello en Python.</span><span class="sxs-lookup"><span data-stu-id="b962d-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="b962d-112">ámbito de Hola de ejemplo de Hola es solamente las notificaciones de toosend limitado y todavía no hace ninguna administración del registro.</span><span class="sxs-lookup"><span data-stu-id="b962d-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="b962d-113">Interfaz del cliente</span><span class="sxs-lookup"><span data-stu-id="b962d-113">Client interface</span></span>
<span data-ttu-id="b962d-114">interfaz de cliente principal de Hello puede proporcionar Hola mismos métodos que están disponibles en hello [.NET SDK de los centros de notificación](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="b962d-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="b962d-115">Esto le permitirá toodirectly traducir todos los tutoriales de Hola y ejemplos, está disponibles en este sitio y aportados por la Comunidad de hello en hello internet.</span><span class="sxs-lookup"><span data-stu-id="b962d-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="b962d-116">Puede encontrar todo el código de hello disponible en hello [ejemplo de contenedor de REST de Python].</span><span class="sxs-lookup"><span data-stu-id="b962d-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="b962d-117">Por ejemplo, toocreate un cliente:</span><span class="sxs-lookup"><span data-stu-id="b962d-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="b962d-118">Introducción a toosend una ventana del sistema notificación:</span><span class="sxs-lookup"><span data-stu-id="b962d-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="b962d-119">Implementación</span><span class="sxs-lookup"><span data-stu-id="b962d-119">Implementation</span></span>
<span data-ttu-id="b962d-120">Si aún no lo hizo, siga nuestro [tutorial introductorio Get] una copia de seguridad toohello última sección donde haya tooimplement Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="b962d-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="b962d-121">Todos Hola tooimplement detalles que se encuentra en un contenedor REST completo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="b962d-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="b962d-122">En esta sección se describen implementación de Python de Hola de hello pasos principales necesarios tooaccess extremos REST de centros de notificaciones y enviar notificaciones</span><span class="sxs-lookup"><span data-stu-id="b962d-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="b962d-123">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="b962d-123">Parse hello connection string</span></span>
2. <span data-ttu-id="b962d-124">Generar el token de autorización de Hola</span><span class="sxs-lookup"><span data-stu-id="b962d-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="b962d-125">Enviar una notificación mediante la API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="b962d-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="b962d-126">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="b962d-126">Parse hello connection string</span></span>
<span data-ttu-id="b962d-127">Aquí es implementar el cliente de hello, cuyo constructor analiza la cadena de conexión de Hola de clase principal de hello:</span><span class="sxs-lookup"><span data-stu-id="b962d-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="b962d-128">Creación del token de seguridad</span><span class="sxs-lookup"><span data-stu-id="b962d-128">Create security token</span></span>
<span data-ttu-id="b962d-129">detalles de Hola de creación de tokens de seguridad de hello [aquí](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="b962d-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="b962d-130">Hello métodos siguientes tienen toobe agregado toohello **NotificationHub** token de Hola de clase toocreate basado en URI de solicitud actual de Hola y las credenciales de hello extraídas de la cadena de conexión de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b962d-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="b962d-131">Enviar una notificación mediante la API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="b962d-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="b962d-132">En primer lugar, definamos una clase que representa una notificación.</span><span class="sxs-lookup"><span data-stu-id="b962d-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="b962d-133">Esta clase es un contenedor para un cuerpo de notificación nativa, o un conjunto de propiedades en el caso de una notificación de plantilla, y un conjunto de encabezados que contienen formato (plataforma o plantilla nativa) y propiedades específicas de la plataforma (como la propiedad de expiración de Apple y los encabezados WNS).</span><span class="sxs-lookup"><span data-stu-id="b962d-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="b962d-134">Consulte toohello [documentación de API de REST de bases de datos centrales de notificación](http://msdn.microsoft.com/library/dn495827.aspx) y Hola formatos de plataformas de notificación específico para todas las opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="b962d-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="b962d-135">Ahora con esta clase, podemos escribir Hola envío métodos de notificación dentro de hello **NotificationHub** clase.</span><span class="sxs-lookup"><span data-stu-id="b962d-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="b962d-136">Hola por encima de los métodos de envío un punto de conexión de HTTP POST solicitud toohello /messages de su centro de notificaciones con cuerpo correcto de Hola y notificación de encabezados toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="b962d-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="b962d-137">Usar depuración propiedad tooenable el registro detallado</span><span class="sxs-lookup"><span data-stu-id="b962d-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="b962d-138">Habilitar la propiedad de depuración al inicializar Hola centro de notificaciones escribirá información de registro detallada sobre Hola HTTP resultado de envío de solicitud y el volcado de respuesta, así como mensaje de notificación detallada.</span><span class="sxs-lookup"><span data-stu-id="b962d-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="b962d-139">Recientemente hemos agregado esta propiedad llama [TestSend de bases de datos centrales de notificación propiedad](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) que devuelve información detallada sobre el resultado de enviar la notificación Hola.</span><span class="sxs-lookup"><span data-stu-id="b962d-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="b962d-140">toouse lo - inicializar usando Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b962d-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="b962d-141">solicitud de envío de concentrador de notificación de Hello dirección URL HTTP se le anexan datos con una cadena de consulta de "prueba" como resultado.</span><span class="sxs-lookup"><span data-stu-id="b962d-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="b962d-142"><a name="complete-tutorial"></a>Tutorial de hello completa</span><span class="sxs-lookup"><span data-stu-id="b962d-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="b962d-143">Ahora puede completar el tutorial de introducción de hello mediante el envío de notificaciones de Hola de un back-end de Python.</span><span class="sxs-lookup"><span data-stu-id="b962d-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="b962d-144">Inicializar el cliente de los centros de notificaciones (sustituya el nombre de concentrador y la cadena de conexión de hello como se indica en hello [tutorial introductorio Get]):</span><span class="sxs-lookup"><span data-stu-id="b962d-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="b962d-145">A continuación, agregue código de envío de hello dependiendo de la plataforma de dispositivos móviles de destino.</span><span class="sxs-lookup"><span data-stu-id="b962d-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="b962d-146">Este ejemplo también agrega tooenable de métodos de nivel superior enviar notificaciones basadas en la plataforma de hello p. ej. send_windows_notification para windows; send_apple_notification (para apple) etcetera.</span><span class="sxs-lookup"><span data-stu-id="b962d-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="b962d-147">Tienda Windows y Windows Phone 8.1 (no Silverlight)</span><span class="sxs-lookup"><span data-stu-id="b962d-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="b962d-148">Silverlight para Windows Phone 8.0 y 8.1</span><span class="sxs-lookup"><span data-stu-id="b962d-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="b962d-149">iOS</span><span class="sxs-lookup"><span data-stu-id="b962d-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="b962d-150">Android</span><span class="sxs-lookup"><span data-stu-id="b962d-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="b962d-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="b962d-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="b962d-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="b962d-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="b962d-153">La ejecución del código Python debe generar una notificación que se mostrará en el dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="b962d-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="b962d-154">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="b962d-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="b962d-155">Habilitar la propiedad de depuración</span><span class="sxs-lookup"><span data-stu-id="b962d-155">Enabling debug property</span></span>
<span data-ttu-id="b962d-156">Cuando se habilita la marca de depuración al inicializar hello NotificationHub verá detallada volcado de solicitud y respuesta HTTP, así como NotificationOutcome como siguiente Hola donde pueda entender qué encabezados HTTP se pasan en la solicitud de Hola y la ruta HTTP se recibió una respuesta de hello centro de notificaciones:![][1]</span><span class="sxs-lookup"><span data-stu-id="b962d-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="b962d-157">El resultado detallado del centro de notificaciones se mostrará, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="b962d-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="b962d-158">al mensaje Hola se envía correctamente toohello servicio de notificaciones Push.</span><span class="sxs-lookup"><span data-stu-id="b962d-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="b962d-159">Si hubiera se encontró ningún destino para las notificaciones de inserción, a continuación, es probable que se van toosee siguiente de Hola en respuesta de hello (que indica que había no se encontraron registros de notificación de hello toodeliver probablemente porque no tenían algunos registros de Hola no coinciden las etiquetas)</span><span class="sxs-lookup"><span data-stu-id="b962d-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="b962d-160">Difusión tooWindows de notificación de notificación del sistema</span><span class="sxs-lookup"><span data-stu-id="b962d-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="b962d-161">Tenga en cuenta los encabezados de Hola que obtengan envía cuando envía un cliente de tooWindows de notificación de sistema de difusión.</span><span class="sxs-lookup"><span data-stu-id="b962d-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="b962d-162">Enviar una notificación que especifica una etiqueta (o expresión de etiqueta)</span><span class="sxs-lookup"><span data-stu-id="b962d-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="b962d-163">Encabezado de HTTP de etiquetas de hello aviso que se agrega la solicitud de toohello HTTP (en el ejemplo de Hola a continuación, se envía Hola notificación solo tooregistrations con una carga de 'deportes')</span><span class="sxs-lookup"><span data-stu-id="b962d-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="b962d-164">Enviar notificación que especifica varias etiquetas</span><span class="sxs-lookup"><span data-stu-id="b962d-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="b962d-165">Observe cómo el encabezado de HTTP de etiquetas de hello cambia cuando se envían varias etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b962d-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="b962d-166">Notificación de plantilla</span><span class="sxs-lookup"><span data-stu-id="b962d-166">Templated notification</span></span>
<span data-ttu-id="b962d-167">Observe que Hola formato HTTP de los cambios y cuerpo de la carga de Hola se envía como parte del cuerpo de la solicitud de hello HTTP:</span><span class="sxs-lookup"><span data-stu-id="b962d-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="b962d-168">**Cliente: plantilla registrada**</span><span class="sxs-lookup"><span data-stu-id="b962d-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="b962d-169">**Servidor - envío de carga de Hola**</span><span class="sxs-lookup"><span data-stu-id="b962d-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="b962d-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b962d-170">Next Steps</span></span>
<span data-ttu-id="b962d-171">En este tema se ha explicado cómo toocreate un simple de Python REST cliente centrales de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="b962d-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="b962d-172">Desde aquí puede:</span><span class="sxs-lookup"><span data-stu-id="b962d-172">From here you can:</span></span>

* <span data-ttu-id="b962d-173">Descargar Hola completa [ejemplo de contenedor de REST de Python], que contiene todo el código de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="b962d-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="b962d-174">Seguir obteniendo información acerca de los centros de notificaciones etiquetado característica Hola [tutorial de noticias de última hora]</span><span class="sxs-lookup"><span data-stu-id="b962d-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="b962d-175">Seguir obteniendo información acerca de la característica de plantillas de bases de datos centrales de notificación en hello [tutorial de noticias localizar]</span><span class="sxs-lookup"><span data-stu-id="b962d-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

