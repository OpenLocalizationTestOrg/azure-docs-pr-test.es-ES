---
title: "autenticación de Service Bus aaaAzure con firmas de acceso compartido | Documentos de Microsoft"
description: "Información general sobre la autenticación en Service Bus con Firma de acceso compartido, detalles de la autenticación con SAS en Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Autenticación en Service Bus con Firmas de acceso compartido

*Firmas de acceso compartido* (SAS) son el mecanismo de seguridad principal de hello para la mensajería de Bus de servicio. Este artículo describe SAS, cómo funcionan y cómo toouse ellas de forma independiente de la plataforma.

Autenticación de SAS permite que las aplicaciones tooauthenticate tooService Bus mediante una clave de acceso configurada en el espacio de nombres de Hola o en hello entidad (cola o tema) de mensajería con qué derechos específicos que están asociados. A continuación, puede usar esta clave toogenerate un token SAS que los clientes pueden usar a su vez tooauthenticate tooService Bus.

Compatibilidad con la autenticación de SAS se incluye en hello Azure SDK versión 2.0 y versiones posterior.

## <a name="overview-of-sas"></a>Información general de SAS

Firmas de acceso compartido son un mecanismo de autenticación basado en URI y valores hash seguros SHA-256. SAS es un mecanismo muy eficaz que se usa por todos los servicios del Bus de servicio. En el uso real, SAS tiene dos componentes: una *directiva de acceso compartido* y una *firma de acceso compartido* (a menudo denominada *token*).

Autenticación con SAS en el Bus de servicio implica la configuración de Hola de una clave criptográfica con derechos asociados en un recurso de Bus de servicio. Los clientes notificación acceso tooService Bus recursos presentando un token SAS. Este token consta del URI que se obtiene acceso de recurso de hello y una fecha de expiración firmada con hello configurado clave.

Puede configurar reglas de autorización de firma de acceso compartido en [retransmisiones](service-bus-fundamentals-hybrid-solutions.md#relays), [colas](service-bus-fundamentals-hybrid-solutions.md#queues) y [temas](service-bus-fundamentals-hybrid-solutions.md#topics) de Service Bus.

La autenticación SAS usa Hola siguientes elementos:

* [Regla de autorización de acceso compartido](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): clave criptográfica principal de 256 bits en representación Base64, una clave secundaria opcional y un nombre de clave y derechos asociados (una colección de derechos de *escucha*, *envío* o *administración*).
* [Firma de acceso compartido](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: generado con hello HMAC-SHA256 de una cadena de recurso, que consta de hello URI del recurso de Hola que se tiene acceso y una fecha de expiración, con la clave criptográfica de Hola. firma de Hola y otros elementos que se describen en las secciones siguientes de hello tienen formato de un saludo de tooform cadena token SAS.

## <a name="shared-access-policy"></a>Directiva de acceso compartido

Una toounderstand importante sobre SAS es que inicia con una directiva. Para cada directiva, decida tres tipos de información: **nombre**, **ámbito** y **permisos**. Hola **nombre** justamente eso; es un nombre único dentro de ese ámbito. Hola ámbito es bastante fácil: Hola de su URI del recurso de hello en cuestión. Un espacio de nombres de Bus de servicio, el ámbito de hello es nombre Hola de dominio completo (FQDN), como `https://<yournamespace>.servicebus.windows.net/`.

permisos disponibles de Hola para una directiva son autoexplicativos en gran medida:

* Los métodos Send
* Escuchar
* Administrar

Después de crear directivas de hello, se asigna un *Primary Key* y un *clave secundaria*. Son claves de alta seguridad criptográfica. No perderlo o la pérdida de ellos: siempre estará disponibles en hello [portal de Azure][Azure portal]. Puede utilizar cualquiera de las claves de hello generado y se puede regenerar en cualquier momento. Sin embargo, si generar o cambiar la clave principal de hello en la directiva de hello, se invalidarán las firmas de acceso compartido creado a partir de él.

Cuando se crea un espacio de nombres de Bus de servicio, automáticamente se crea una directiva para hello todo espacio de nombres denominado **RootManageSharedAccessKey**, y esta directiva tiene todos los permisos. No inicia sesión como **raíz**; por tanto, no use esta directiva a menos que exista realmente una buena razón. También puede crear directivas adicionales en hello **configurar** pestaña de espacio de nombres de hello en el portal de Hola. Es importante toonote que sólo puede tener un nivel del árbol único en el Bus de servicio (espacio de nombres, cola, etc.) hasta too12 las directivas adjuntas tooit.

## <a name="configuration-for-shared-access-signature-authentication"></a>Configuración de la autenticación de firma de acceso compartido
Puede configurar hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) regla en espacios de nombres de Bus de servicio, colas o temas. Configurar un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) en un Bus de servicio de suscripción no se admite actualmente, pero puede usar las reglas configuradas en un toosubscriptions de acceso de toosecure de espacio de nombres o un tema. Para obtener un ejemplo funcional que muestra este procedimiento, vea hello [autenticación de uso de firma de acceso compartido (SAS) con suscripciones de Bus de servicio](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) ejemplo.

Puede configurarse un máximo de 12 reglas en un espacio de nombres, una cola o un tema del Bus de servicio. Las reglas que se configuran en un espacio de nombres de Bus de servicio aplican las entidades tooall en ese espacio de nombres.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

En esta ilustración, Hola *manageRuleNS*, *sendRuleNS*, y *listenRuleNS* tooboth cola Q1 y tema T1, aplican las reglas de autorización mientras *listenRuleQ*  y *sendRuleQ* aplicar solo tooqueue Q1 y *sendRuleT* se aplica solo tootopic T1.

Hola parámetros principales de un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) son los siguientes:

| Parámetro | Descripción |
| --- | --- |
| *KeyName* |Una cadena que describe la regla de autorización de Hola. |
| *PrimaryKey* |Una codificación base64 de 256 bits clave principal para firmar y validar el token de SAS de Hola. |
| *SecondaryKey* |Una con codificación base64 de 256 bits clave secundaria para firmar y validar el token de SAS de Hola. |
| *AccessRights* |Una lista de derechos de acceso concedidos por la regla de autorización de Hola. Estos derechos pueden ser cualquier colección de derechos de escucha, envío y administración. |

Cuando se aprovisiona un espacio de nombres de Bus de servicio, un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), con [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) establecido demasiado**RootManageSharedAccessKey**, se crea de forma predeterminada.

## <a name="generate-a-shared-access-signature-token"></a>Generación de firmas de acceso compartido (tokens)

Hola propia directiva no es el token de acceso de Hola para Bus de servicio. Es objeto de Hola desde qué Hola se genera el token de acceso - mediante la clave principal o secundaria Hola. Cualquier cliente que tiene toohello de acceso especificadas en la regla de autorización de acceso compartido de Hola de claves de firma puede generar el token de SAS de Hola. símbolo (token) de Hello genera reflexionar profundamente sobre una cadena en hello siguiendo el formato:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Donde `signature-string` es hash Hola SHA-256 de ámbito de hello del token de hello (**ámbito** tal y como se describe en la sección anterior de hello) con un CRLF anexado y una hora de expiración (en segundos transcurridos desde la época de hello: `00:00:00 UTC` de 1 de enero de 1970). 

> [!NOTE]
> tooavoid una hora de caducidad del token corto, se recomienda que codificar el valor de hora de expiración de hello como al menos un entero de 32 bits sin signo o, preferiblemente en un entero largo (64 bits).  
> 
> 

hash de Hello parece similar toohello siguiente pseudocódigo y devuelve 32 bytes.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

valores de Hello no aplica un algoritmo hash que se encuentran en hello **SharedAccessSignature** de cadena para que hello destinatario puede calcular el hash de hello con hello toobe seguro de que se devuelven los mismos parámetros Hola el mismo resultado. Hola URI especifica el ámbito de Hola y nombre de clave de hello identifica Hola directiva toobe utiliza toocompute Hola hash. Esto es importante desde una perspectiva de seguridad. Si firma hello no coincide con la que calcula qué destinatario hello (Service Bus), se deniega el acceso. En este momento se puede conocer ese remitente Hola tenía la clave de acceso toohello y debe tener derechos de hello especificado en la directiva de Hola.

Tenga en cuenta que debe usar el URI de recurso de hello codificado para esta operación. URI de recurso de Hello es hello que se notifica el URI completo de hello acceso a Service Bus toowhich los recursos. Por ejemplo, `http://<namespace>.servicebus.windows.net/<entityPath>` o `sb://<namespace>.servicebus.windows.net/<entityPath>`; es decir, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

regla de autorización de acceso compartido Hola usada para firmar debe configurarse en la entidad de hello especificada por este identificador URI, o en uno de sus elementos primarios jerárquicos. Por ejemplo, `http://contoso.servicebus.windows.net/contosoTopics/T1` o `http://contoso.servicebus.windows.net` en el ejemplo anterior de Hola.

Un token SAS es válido para todos los recursos en hello `<resourceURI>` utilizados en hello `signature-string`.

Hola [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) en hello SAS token refiere toohello **keyName** de hello regla de autorización de acceso compartido utiliza símbolo (token) de toogenerate Hola.

Hola *URL-encoded-resourceURI* debe Hola igual Hola URI que se usa en string-to-sign de Hola durante el cálculo de Hola de firma de Hola. Debe estar [codificado por porcentaje](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Se recomienda regenerar periódicamente las claves de hello utilizadas en hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto. Las aplicaciones deben utilizar generalmente hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate un token de SAS. Al volver a generar las claves de hello, debe reemplazar hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) con principal antiguo Hola clave y generar una nueva clave como la nueva clave principal de Hola. Esto le permite toocontinue mediante tokens de autorización que se emitieron con la clave principal antigua de Hola y que aún no haya expirado.

Si una clave está en peligro y tiene toorevoke Hola claves, puede volver a generar ambos hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) hello y [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) de un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), reemplazarlos con nuevas claves. Este procedimiento invalida todos los tokens firmados con claves antiguas Hola.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>¿Cómo toouse autenticación de firma de acceso compartido con Bus de servicio

Hola los escenarios siguientes están la configuración de reglas de autorización y la generación de tokens de SAS y la autorización de cliente.

Para un completo ejemplo funcional de una aplicación de Bus de servicio que muestra la autorización de SAS de configuración y usa hello, consulte [autenticación de firma de acceso compartido con Bus de servicio](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Un ejemplo relacionado que se muestra el uso de Hola de reglas de autorización de SAS configuradas en los espacios de nombres o temas suscripciones del Bus de servicio toosecure está disponible aquí: [autenticación de uso de firma de acceso compartido (SAS) con suscripciones de Bus de servicio ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Acceso a las reglas de autorización de acceso compartido en un espacio de nombres

Operaciones en la raíz de espacio de nombres de Bus de servicio de hello requerir autenticación de certificado. Debe cargar un certificado de administración para la suscripción de Azure. tooupload un certificado de administración, siga los pasos de hello [aquí](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), con hello [portal de Azure][Azure portal]. Para obtener más información acerca de los certificados de administración de Azure, vea hello [Introducción a los certificados de Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

punto de conexión de Hello para tener acceso a las reglas de autorización de acceso compartido en un espacio de nombres de Bus de servicio es el siguiente:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate una [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) de objetos en un espacio de nombres de Bus de servicio, ejecute una operación POST en este punto de conexión con la información de la regla de hello serializada como JSON o XML. Por ejemplo:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Asimismo, utilice una operación GET en hello extremo tooread hello las reglas de autorización configuradas en el espacio de nombres de Hola.

tooupdate o eliminar una regla de autorización específica, use Hola después de punto de conexión:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Acceso a las reglas de autorización de acceso compartido en una entidad

Puede tener acceso a un [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto configurado en una cola de Bus de servicio o un tema a través de hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) colección Hola correspondiente [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) o [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Hola siguiente código muestra cómo las reglas de autorización de tooadd para una cola.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Uso de la autorización de la firma de acceso compartido

Uso hello Azure SDK para .NET con las bibliotecas de .NET de Bus de servicio de hello las aplicaciones pueden utilizar la autorización de SAS a través de hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) clase. Hello siguiente código muestra hello uso de cola de Bus de servicio de tooa de mensajes de Hola proveedor de tokens toosend.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Las aplicaciones también pueden usar SAS para la autenticación mediante una cadena de conexión SAS en métodos que acepten cadenas de conexión.

Tenga en cuenta esa autorización de SAS toouse con las retransmisiones de Bus de servicio, puede usar claves de SAS configuradas en el espacio de nombres de Bus de servicio de Hola. Si crea explícitamente una retransmisión en el espacio de nombres de hello ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) con un [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) del objeto, puede establecer reglas SAS de Hola para dicha retransmisión. toouse autorización de SAS con suscripciones de Bus de servicio, puede usar claves de SAS configuradas en un espacio de nombres de Bus de servicio o en un tema.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Usar hello firma de acceso compartido (en el nivel HTTP)

Ahora que sabe cómo toocreate firmas de acceso compartido para todas las entidades de Bus de servicio, está listo tooperform una solicitud HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Recuerde que esto funciona para todo. Puede crear SAS para una cola, un tema o una suscripción. 

Si se concede a un remitente o cliente un token de SAS, no tienen clave Hola directamente y no es posible revertir Hola hash tooobtain lo. Como tal, tiene control sobre a lo que pueden tener acceso y durante cuánto tiempo. Un tooremember lo importante es que si cambia la clave principal de hello en la directiva de hello, se invalidarán las firmas de acceso compartido creado a partir de él.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Usar hello firma de acceso compartido (en el nivel AMQP)

En la sección anterior de hello, ha visto cómo toouse Hola token SAS con una solicitud HTTP POST para enviar datos toohello Bus de servicio. Como sabe, puede tener acceso a Service Bus utilizando Hola Advanced Message Queuing Protocol (AMQP), es toouse de protocolo de hello preferido por motivos de rendimiento en muchos escenarios. Hola uso del token de SAS con AMQP se describe en el documento de hello [AMQP Claim-Based seguridad versión 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) decir en borrador de trabajo a partir de 2013 pero ampliamente admitido por Azure hoy en día.

Antes de iniciar toosend datos tooService Bus, Hola publicador tiene que enviar token SAS de hello dentro de un AMQP mensaje tooa bien definidos AMQP nodo denominado **$cbs** (puede ver como una cola "especial" utilizada por tooacquire de servicio de Hola y todas las validar tokens SAS Hello). publicador de Hello debe especificar hello **ReplyTo** campo dentro del mensaje de Hola AMQP; se trata de nodo de hello en qué Hola servicio responde toohello publicador con el resultado de hello de validación de tokens de hello (un sencillo modelo solicitud-respuesta entre publicador y el servicio). Se crea este nodo de respuesta "en hello marcha," habla sobre "creación dinámica de nodo remoto", como se describe en la especificación de hello AMQP 1.0. Después de comprobar que ese token SAS hello es válido, publisher Hola puede avanzar e iniciar servicio toohello de toosend datos.

Hello pasos siguientes muestran cómo toosend Hola token de SAS con protocolo AMQP con hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) biblioteca. Esto es útil si no se puede utilizar oficial de hello SDK del Bus de servicio (por ejemplo, en WinRT, .net Compact Framework, .net Framework Micro y Mono) desarrollar en C\#. Por supuesto, esta biblioteca es útil toohelp comprender la seguridad basada en notificaciones cómo funciona en el nivel AMQP de hello, tal como se ha visto cómo funciona en el nivel de hello HTTP (con un encabezado HTTP POST hello y solicitud de SAS token Hola enviado dentro de "Autorización"). Si no es necesario este tipo profundo conocimiento acerca de AMQP, puede usar oficial de hello SDK de Service Bus con .net las aplicaciones de Framework, lo hará por usted.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hola `PutCbsToken()` método recibe hello *conexión* (instancia de la clase de la conexión AMQP proporcionados por hello [AMQP .NET Lite biblioteca](https://github.com/Azure/amqpnetlite)) que representa el servicio de toohello de conexión de TCP de Hola y Hola *sasToken* parámetro hello SAS token toosend. 

> [!NOTE]
> Es importante que la conexión de Hola se crea con **mecanismo de autenticación SASL establece tooEXTERNAL** (y no Hola simple de forma predeterminada con el nombre de usuario y contraseña que se usa cuando no se necesitan token de SAS de hello toosend).
> 
> 

A continuación, el publicador de hello crea dos vínculos AMQP para enviar el token de SAS de Hola y reciben respuesta hello (resultado de validación del token de hello) de servicio de Hola.

mensaje de bienvenida de AMQP contiene un conjunto de propiedades y más información que un mensaje sencillo. token SAS de Hello es cuerpo Hola de mensaje de saludo (mediante su constructor). Hola **"ReplyTo"** propiedad está establecida en nombre del nodo toohello para recibir el resultado de la validación de hello en vínculo de receptor de hello (puede cambiar su nombre si desea y se creará dinámicamente por el servicio de hello). Hello propiedades de aplicación/personalizada tres últimas usan Hola servicio tooindicate qué tipo de operación tiene tooexecute. Como se describe en hello borrador de especificación de CBS, deben ser hello **nombre de la operación** ("put-token"), hello **tipo de token** (en este caso, un "servicebus.windows.net:sastoken"), hello y **" nombre"de audiencia de hello** (Hola toda la entidad) aplica el token de hello toowhich.

Después de enviar el token de SAS de hello en el vínculo de remitente de hello, publisher Hola debe leer la respuesta de hello en el vínculo de receptor de Hola. Hola de respuesta es un mensaje AMQP simple con una propiedad de la aplicación denominada **"código de estado"** que puede contener Hola mismo valores como un código de estado HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Derechos necesarios para realizar operaciones del Bus de servicio

Hello tabla siguiente muestran los derechos de acceso de hello necesarios para realizar diversas operaciones en recursos de Bus de servicio.

| Operación | Solicitud necesaria | Ámbito de solicitud |
| --- | --- | --- |
| **Espacio de nombres** | | |
| Configurar la regla de autorización en un espacio de nombres |administración |Cualquier dirección de espacio de nombres |
| **Registro del servicio** | | |
| Enumerar directivas privadas |administración |Cualquier dirección de espacio de nombres |
| Empezar a escuchar en un espacio de nombres |Escuchar |Cualquier dirección de espacio de nombres |
| Enviar el agente de escucha de mensajes tooa en un espacio de nombres |Los métodos Send |Cualquier dirección de espacio de nombres |
| **Cola** | | |
| Creación de una cola |administración |Cualquier dirección de espacio de nombres |
| Eliminación de una cola |administración |Cualquier dirección de cola válida |
| Enumerar colas |administración |/$Resources/Queues |
| Obtener la descripción de la cola de Hola |Administrar |Cualquier dirección de cola válida |
| Configurar la regla de autorización para una cola |administración |Cualquier dirección de cola válida |
| Enviar a la cola de toohello |Los métodos Send |Cualquier dirección de cola válida |
| mensajes de una cola |Escuchar |Cualquier dirección de cola válida |
| Abandonar o completar mensajes después de recibir el mensaje de bienvenida en modo de bloqueo de inspección |Escuchar |Cualquier dirección de cola válida |
| Aplazar un mensaje para su recuperación posterior |Escuchar |Cualquier dirección de cola válida |
| Mensaje fallido |Escuchar |Cualquier dirección de cola válida |
| Obtener estado de hello asociado a una sesión de cola de mensajes |Escuchar |Cualquier dirección de cola válida |
| Estado de hello conjunto asociado a una sesión de cola de mensajes |Escuchar |Cualquier dirección de cola válida |
| **Tema.** | | |
| de un tema |administración |Cualquier dirección de espacio de nombres |
| Eliminación de un tema |administración |Cualquier dirección de tema válida |
| Enumerar temas |administración |/$Resources/Topics |
| Obtener la descripción del tema Hola |Administrar |Cualquier dirección de tema válida |
| Configurar la regla de autorización para un tema |administración |Cualquier dirección de tema válida |
| Enviar tema toohello |Los métodos Send |Cualquier dirección de tema válida |
| **Suscripción** | | |
| una suscripción |administración |Cualquier dirección de espacio de nombres |
| Eliminar suscripción |administración |../myTopic/Subscriptions/mySubscription |
| Enumerar suscripciones |administración |../myTopic/Subscriptions |
| Obtener la descripción de la suscripción |Administrar |../myTopic/Subscriptions/mySubscription |
| Abandonar o completar mensajes después de recibir el mensaje de bienvenida en modo de bloqueo de inspección |Escuchar |../myTopic/Subscriptions/mySubscription |
| Aplazar un mensaje para su recuperación posterior |Escuchar |../myTopic/Subscriptions/mySubscription |
| Mensaje fallido |Escuchar |../myTopic/Subscriptions/mySubscription |
| Obtener estado de hello asociado a una sesión de tema |Escuchar |../myTopic/Subscriptions/mySubscription |
| Definir estado de hello asociado a una sesión de tema |Escuchar |../myTopic/Subscriptions/mySubscription |
| **Reglas** | | |
| Crear una regla |administración |../myTopic/Subscriptions/mySubscription |
| Eliminar una regla |administración |../myTopic/Subscriptions/mySubscription |
| Enumerar reglas |Administrar o escuchar |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de la mensajería de Bus de servicio, vea Hola temas siguientes.

* [Elementos fundamentales de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Colas, temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md)
* [¿Cómo toouse colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [¿Cómo toouse Service Bus temas y suscripciones](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com