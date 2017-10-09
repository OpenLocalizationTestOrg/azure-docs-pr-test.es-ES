---
title: seguridad de Azure IoT Hub aaaUnderstand | Documentos de Microsoft
description: "Guía para desarrolladores - cómo toocontrol acceso tooIoT concentrador para aplicaciones de dispositivos y aplicaciones de back-end. Además, incluye información sobre los tokens de seguridad y la compatibilidad con certificados X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Controlar el acceso tooIoT concentrador

En este artículo se describe las opciones de Hola para proteger su centro de IoT. Centro de IoT usa *permisos* toogrant punto de conexión de acceso tooeach IoT hub. Permisos de limitan el centro de IoT tooan Hola acceso basado en la funcionalidad.

En este artículo se describe:

* Hola distintos permisos que puede conceder tooa dispositivos o aplicaciones back-end tooaccess su centro de IoT.
* Hola tokens hello y proceso de autenticación utiliza tooverify permisos.
* ¿Cómo tooscope credenciales toolimit acceder a los recursos de toospecific.
* IoT Hub admite los certificados X.509.
* Los mecanismos de autenticación de dispositivo personalizado que utilizan los registros de identidad de dispositivo o los esquemas de autenticación.

### <a name="when-toouse"></a>Cuando toouse

Debe tener los permisos adecuados tooaccess cualquiera de los extremos del centro de IoT Hola. Por ejemplo, un dispositivo debe incluir un símbolo (token) que contiene las credenciales de seguridad junto con cada mensaje que envía tooIoT concentrador.

## <a name="access-control-and-permissions"></a>Permisos y control del acceso

Puede conceder [permisos](#iot-hub-permissions) Hola siguientes maneras:

* **Directivas de acceso compartido de nivel de centro de IoT**. Las directivas de acceso compartido pueden conceder cualquier combinación de los [permisos](#iot-hub-permissions). Las directivas se pueden definir en hello [portal de Azure][lnk-management-portal], o mediante programación usando hello [API de REST de proveedor de recursos de centro de IoT][lnk-resource-provider-apis]. Un centro de IoT recién creado tiene Hola siguiendo las directivas predeterminadas:

  * **iothubowner**: directiva con todos los permisos.
  * **service**: directiva con el permiso **ServiceConnect**.
  * **device**: directiva con el permiso **DeviceConnect**.
  * **registryRead**: directiva con el permiso **RegistryRead**.
  * **registryReadWrite**: directiva con los permisos **RegistryRead** y RegistryWrite.
  * **Credenciales de seguridad de cada dispositivo**. Cada centro de IoT contiene un [registro de identidades][lnk-identity-registry]. Para cada dispositivo en este registro de identidad, puede configurar las credenciales de seguridad que concedan **DeviceConnect** toohello puntos de conexión de dispositivo correspondientes del ámbito de permisos.

Por ejemplo en una solución típica de IoT:

* componente de administración de dispositivos de Hello usa hello *registryReadWrite* directiva.
* componente del procesador de eventos de Hello usa hello *servicio* directiva.
* componente de lógica de negocios de Hello dispositivo de tiempo de ejecución utiliza hello *servicio* directiva.
* Dispositivos individuales se conectan mediante las credenciales almacenadas en el registro de la identidad del centro de IoT de Hola.

> [!NOTE]
> Para más detalles, vea [Permisos](#iot-hub-permissions).

## <a name="authentication"></a>Autenticación

Centro de IoT de Azure, se concede acceso tooendpoints comprobando un token con las directivas de acceso compartido de Hola y credenciales de identidad de seguridad del registro.

Las credenciales de seguridad, como las claves simétricas, nunca se envían a través de la conexión de Hola.

> [!NOTE]
> Hello proveedor de recursos de centro de IoT de Azure se protege mediante la suscripción de Azure, igual que todos los proveedores de hello [Azure Resource Manager][lnk-azure-resource-manager].

Para obtener más información acerca de cómo tooconstruct y use tokens de seguridad, vea [tokens de seguridad del centro de IoT][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Detalles específicos de protocolo

Cada protocolo admitido, como MQTT, AMQP y HTTP, transporta tokens de diferentes maneras.

Cuando se usa MQTT, paquete de saludo conectar tiene deviceId Hola Hola ClientId, {iothubhostname} / {deviceId} en el campo de nombre de usuario de Hola y un token SAS en el campo de contraseña de Hola. {iothubhostname} debe ser Hola CName completa del centro de IoT hello (por ejemplo, contoso.azure-devices.net).

Al usar [AMQP][lnk-amqp], IoT Hub admite [SASL PLAIN][lnk-sasl-plain] y [seguridad basada en notificaciones AMQP][lnk-cbs].

Si usa AMQP notificaciones según-seguridad, Hola estándar especifica cómo tootransmit estos tokens.

Para SASL sin formato, Hola **nombre de usuario** puede ser:

* `{policyName}@sas.root.{iothubName}` si usa tokens de nivel de centro de IoT.
* `{deviceId}@sas.{iothubname}` si usa tokens de ámbito por el dispositivo.

En ambos casos, campo de contraseña de Hola contiene el token de hello, como se describe en [tokens de seguridad del centro de IoT][lnk-sas-tokens].

HTTP implementa la autenticación mediante la inclusión de un token válido en hello **autorización** encabezado de solicitud.

#### <a name="example"></a>Ejemplo

Nombre de usuario (DeviceId distingue entre mayúsculas y minúsculas): `iothubname.azure-devices.net/DeviceId`

Contraseña (token de SAS generar con hello [explorer dispositivo] [ lnk-device-explorer] herramienta):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Hola [SDK de Azure IoT] [ lnk-sdks] automáticamente generar tokens cuando se conecta el servicio toohello. En algunos casos, hello Azure IoT SDK no son compatibles con todos los protocolos de Hola o todos los métodos de autenticación de Hola.

### <a name="special-considerations-for-sasl-plain"></a>Consideraciones especiales para SASL PLAIN

Cuando se usa sin formato SASL con AMQP, un cliente que se conecta el centro de IoT tooan puede usar un token único para cada conexión TCP. Cuando expira el token de hello, Hola conexión TCP se desconecta del servicio de Hola y desencadena una reconexión. Este comportamiento, aunque no problemático para una aplicación back-end, es perjudicial para una aplicación de dispositivo para hello siguientes motivos:

* Las puertas de enlace normalmente se conectan en nombre de muchos dispositivos. Cuando se usa sin formato SASL, tienen toocreate una conexión TCP distinta para cada dispositivo que se conecta el centro de IoT tooan. Este escenario considerablemente aumenta el consumo de hello potencia y recursos de red y aumenta la latencia de Hola de cada conexión de dispositivo.
* Dispositivos de recursos restringidos se ven afectados negativamente mediante el uso de hello aumentado de recursos tooreconnect después de cada vencimiento del token.

## <a name="scope-iot-hub-level-credentials"></a>Restricción de las credenciales de nivel de centro de IoT

Puede restringir el ámbito de las directivas de seguridad de nivel de centro de IoT mediante la creación de tokens con un URI de recurso restringido. Por ejemplo, mensajes de Hola extremo toosend dispositivo a la nube desde un dispositivo es **/devices/ {deviceId} / mensajes y eventos**. También puede utilizar una directiva de acceso compartido de nivel del centro de IoT con **DeviceConnect** permisos toosign un token es cuyo resourceURI **/devices/ {deviceId}**. Este método crea un símbolo (token) que solo se puede usar toosend mensajes en nombre de dispositivo **deviceId**.

Este mecanismo es similar toohello [directiva de edición de los centros de eventos][lnk-event-hubs-publisher-policy]y permite los métodos de autenticación personalizados de tooimplement.

## <a name="security-tokens"></a>Tokens de seguridad

Centro de IoT utiliza la seguridad de tokens tooauthenticate dispositivos y servicios tooavoid envío de claves en el cable Hola. Además, los tokens de seguridad están limitados en cuanto al ámbito y el período de validez. Los [SDK IoT de Azure][lnk-sdks] generan automáticamente tokens sin necesidad de ninguna configuración especial. Algunos escenarios requieren toogenerate y utilizar directamente los tokens de seguridad. Entre los escenarios se incluyen los siguientes:

* uso directo de Hola de superficies de hello MQTT, AMQP o HTTP.
* Hola implementación del modelo de servicio de token de hello, como se explica en [autenticación de dispositivo personalizada][lnk-custom-auth].

Centro de IoT también permite tooauthenticate de dispositivos con el centro de IoT con [certificados X.509][lnk-x509].

### <a name="security-token-structure"></a>Estructura del token de seguridad

Usar seguridad tokens toogrant acceso limitado de tiempo toodevices toospecific funcionalidad de servicios y en el centro de IoT. tooget autorización tooconnect tooIoT concentrador, dispositivos y servicios deben enviar los tokens de seguridad firmados con un acceso compartido o una clave simétrica. Dichas claves están almacenadas con una identidad de dispositivo en el registro de la identidad de Hola.

Un token firmado con una funcionalidad de hello acceso compartido clave concede acceso tooall asociada con permisos de directiva de acceso de hello compartido. Un token firmado con hello de concesiones única clave simétrica de la identidad de dispositivo **DeviceConnect** permiso para hello asociados identidad del dispositivo.

token de seguridad de Hello tiene Hola siguiendo el formato:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Estos son los valores esperados hello:

| Valor | Description |
| --- | --- |
| {signature} |Una cadena de firma de HMAC-SHA256 del formulario de hello: `{URL-encoded-resourceURI} + "\n" + expiry`. **Importante**: clave hello es descodificar de base64 y se utiliza como clave tooperform cálculo de hello HMAC-SHA256. |
| {resourceURI} |Prefijo URI (por segmento) de los puntos de conexión de Hola que puede tener acceso a este token, empezando por el nombre de host del centro de IoT hello (ningún protocolo). Por ejemplo: `myHub.azure-devices.net/devices/device1` |
| {expiry} |UTF8 cadenas para el número de segundos transcurridos desde la época de hello 00:00:00 hora UTC de 1 de enero de 1970. |
| {URL-encoded-resourceURI} |Cuanto menor sea caso codificación de direcciones URL de URI de recurso de minúsculas Hola |
| {policyName} |nombre de Hola de hello compartido toowhich de directiva de acceso que hace referencia este token. Está ausente if token Hola hace referencia a las credenciales de registro toodevice. |

**Tenga en cuenta en el prefijo**: prefijo URI de Hola se calcula por segmento y no por carácter. Por ejemplo `/a/b` es un prefijo de `/a/b/c` pero `/a/bc`.

Hello Node.js fragmento siguiente muestra una función denominada **generateSasToken** que calcula Hola símbolo (token) de entradas de hello `resourceUri, signingKey, policyName, expiresInMins`. Hola siguiente se detallan cómo tooinitialize Hola diferentes entradas token distinto de hello utilizar casos.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Como comparación, Hola toogenerate equivalente de código de Python que es un token de seguridad:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Puesto que el periodo de validez de Hola de token de Hola se valida en equipos de centro de IoT, una desviación de hello en reloj Hola de máquina de Hola que genera el token de hello debe ser mínima.

### <a name="use-sas-tokens-in-a-device-app"></a>Uso de tokens de SAS en una aplicación de dispositivo

Hay tooobtain de dos maneras **DeviceConnect** permisos con el centro de IoT con tokens de seguridad: usar un [clave simétrica dispositivo desde el registro de la identidad de hello](#use-a-symmetric-key-in-the-identity-registry), o usar un [declavedeaccesocompartido](#use-a-shared-access-policy).

Recuerde que puede acceder a toda la funcionalidad desde los dispositivos expuestos por diseño en los puntos de conexión con el prefijo `/devices/{deviceId}`.

> [!IMPORTANT]
> Hola única manera de que el centro de IoT autentica un dispositivo específico está usando la clave simétrica de identidad de dispositivo de Hola. En casos cuando una directiva de acceso compartido es tooaccess usa funcionalidad del dispositivo, solución de hello debe tener en cuenta componente Hola emisión de token de seguridad de Hola como un subcomponente de confianza.

los puntos de conexión del dispositivo de Hello son (independientemente del protocolo de hello):

| Extremo | Funcionalidad |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Envío de mensajes de dispositivo a nube. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Recepción de mensajes de nube a dispositivo |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Usar una clave simétrica en el registro de la identidad de Hola

Cuando se usa toogenerate clave simétrica un token de una identidad dispositivo, Hola policyName (`skn`) se omite el elemento de token de Hola.

Por ejemplo, crea un token de tooaccess toda la funcionalidad de dispositivo debe haber Hola parámetros siguientes:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* clave de firma: cualquier clave simétrica para hello `{device id}` identidad,
* ningún nombre de directiva,
* cualquier fecha de expiración.

Un ejemplo de cómo utilizar Hola anterior Node.js función sería:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

resultado de Hello, que concede acceso a la funcionalidad de tooall para dispositivo1, sería:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Es posible toogenerate un token SAS mediante .NET hello [explorador del dispositivo] [ lnk-device-explorer] herramienta u Hola multiplataforma, basado en nodos [el centro de IOT explorador] [ lnk-iothub-explorer] utilidad de línea de comandos.

### <a name="use-a-shared-access-policy"></a>Uso de una directiva de acceso compartido

Cuando se crea un símbolo (token) de una directiva de acceso compartido, establezca hello `skn` toohello nombre del campo de directiva de Hola. Esta directiva debe conceder hello **DeviceConnect** permiso.

Hola dos escenarios principales para usar la funcionalidad de dispositivo de tooaccess de directivas de acceso compartido son:

* [puertas de enlace del protocolo en la nube][lnk-endpoints],
* [Servicios de tokens] [ lnk-custom-auth] utiliza esquemas de autenticación personalizados de tooimplement.

Desde Hola directiva de acceso compartido puede potencialmente conceder acceso tooconnect como cualquier dispositivo, es importante toouse Hola correcta URI del recurso al crear tokens de seguridad. Esta opción es especialmente importante para los servicios de token, que tienen con el URI de recurso de hello tooscope hello tooa token específico dispositivo. Este punto es menos relevante para puertas de enlace de protocolo, puesto que ya están mediando el tráfico para todos los dispositivos.

Por ejemplo, un servicio de token con hello creado previamente compartido llama a la directiva de acceso **dispositivo** crearía un token con hello parámetros siguientes:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* clave de firma: una de las claves de Hola de hello `device` directiva,
* nombre de la directiva: `device`,
* cualquier fecha de expiración.

Un ejemplo de cómo utilizar Hola anterior Node.js función sería:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

resultado de Hello, que concede acceso a la funcionalidad de tooall para dispositivo1, sería:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Una puerta de enlace de protocolo podría utilizar Hola mismo símbolo (token) para todos los dispositivos que simplemente establecer Hola URI de recurso demasiado`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Uso de tokens de seguridad de los componentes de servicio

Componentes del servicio solo pueden generar tokens de seguridad mediante las directivas de acceso compartido para conceder los permisos adecuados de hello tal y como se ha explicado anteriormente.

Aquí está expuestas en los puntos de conexión de hello las funciones de servicios de hello:

| Extremo | Funcionalidad |
| --- | --- |
| `{iot hub host name}/devices` |Creación, actualización, recuperación y eliminación de las identidades del dispositivo. |
| `{iot hub host name}/messages/events` |Recepción de mensajes de dispositivo a nube. |
| `{iot hub host name}/servicebound/feedback` |Recepción de comentarios para los mensajes de nube a dispositivo. |
| `{iot hub host name}/devicebound` |Envío de mensajes de nube a dispositivo. |

Por ejemplo, un servicio que se genera utilizando Hola creado previamente compartido llama a la directiva de acceso **registryRead** crearía un token con hello parámetros siguientes:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices`,
* clave de firma: una de las claves de Hola de hello `registryRead` directiva,
* nombre de la directiva: `registryRead`,
* cualquier fecha de expiración.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

resultado de Hello, que le concede acceso tooread todas las identidades del dispositivo, sería:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Certificados X.509 compatibles

Puede usar cualquier tooauthenticate de certificado X.509 un dispositivo con el centro de IoT. Los certificados incluyen:

* **Un certificado X.509 existente**. Puede que un dispositivo ya tenga un certificado X.509 asociado. dispositivo de Hello puede usar este certificado tooauthenticate con centro de IoT.
* **Un certificado X-509 autofirmado y generado automáticamente**. Un fabricante del dispositivo o implementador interna puede generar estos certificados y almacenar Hola clave privada correspondiente (y el certificado) en el dispositivo de Hola. Puede usar herramientas como [OpenSSL][lnk-openssl] y la utilidad [Windows SelfSignedCertificate][lnk-selfsigned] para este propósito.
* **Certificado X.509 firmado por una CA**. tooidentify un dispositivo y autenticar con el centro de IoT, puede usar un certificado X.509 generado y firmado por una entidad de certificación (CA). Centro de IoT solo comprueba esa huella digital de hello presentado coincide con la huella digital de hello configurado. El centro de IOT no valida la cadena de certificados de Hola.

Un dispositivo puede usar un token de seguridad o un certificado X.509 para realizar la autenticación, pero no ambos.

### <a name="register-an-x509-certificate-for-a-device"></a>Registro de certificados X.509 en un dispositivo

Hola [SDK del servicio de IoT de Azure para C#] [ lnk-service-sdk] (versión 1.0.8+) admite registrar un dispositivo que usa un certificado X.509 para la autenticación. Otras API como la importación y exportación de dispositivos también admiten este tipo de certificados.

### <a name="c-support"></a>Compatibilidad con C\#

Hola **RegistryManager** clase proporciona un mecanismo de programación tooregister un dispositivo. En concreto, Hola **AddDeviceAsync** y **UpdateDeviceAsync** métodos permiten tooregister y actualizar un dispositivo en hello del registro de identidad de centro de IoT. Estos dos métodos toman una instancia **Device** como entrada. Hola **dispositivo** clase incluye una **autenticación** propiedad que permite toospecify principales y secundarias X.509 huellas digitales de certificado. huella digital de Hello representa un hash SHA-1 del certificado X.509 de hello (almacenada mediante codificación DER binaria). Tiene la opción de Hola de especificar una huella digital del principal o una huella digital del secundaria o ambos. Huellas digitales principales y secundarias son escenarios de sustitución de certificados toohandle admitidos.

> [!NOTE]
> Centro de IoT no requiere ni almacenar certificado X.509 completo hello, sólo huella digital de Hola.

Este es un ejemplo C\# un dispositivo mediante un certificado X.509 de tooregister de fragmento de código:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Uso de certificados X.509 durante las operaciones en entorno de ejecución

Hola [dispositivos de IoT de Azure SDK para .NET] [ lnk-client-sdk] (versión 1.0.11+) admite el uso de Hola de certificados X.509.

### <a name="c-support"></a>Compatibilidad con C\#

Hola clase **DeviceAuthenticationWithX509Certificate** admite Hola creación de **DeviceClient** instancias mediante un certificado X.509. certificado X.509 de Hello debe estar en formato PFX (también llamado PKCS #12) de Hola que incluye la clave privada de Hola.

A continuación, veremos un fragmento de código de ejemplo:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Personalización de la autenticación de dispositivos

Puede usar hello centro de IoT [del registro de identidad] [ lnk-identity-registry] las credenciales de seguridad de tooconfigure por dispositivo y control de acceso usando [tokens] [ lnk-sas-tokens] . Si una solución de IoT ya tiene un esquema de registro o la autenticación de identidad personalizado, considere la posibilidad de crear un *del servicio de token* toointegrate esta infraestructura con el centro de IoT. De este modo, puede usar otras características de IoT en la solución.

Un servicio de token es un servicio en la nube personalizado. Usa un centro de IoT *directiva de acceso compartido* con **DeviceConnect** permisos toocreate *centrada en el dispositivo* símbolos (tokens). Estos tokens habilitar un centro de IoT de dispositivo tooconnect tooyour.

![Pasos del modelo de servicio de token de Hola][img-tokenservice]

Estos son Hola pasos principales del modelo de servicio de token de hello:

1. Cree una directiva de acceso compartido de IoT Hub con permisos **DeviceConnect** para IoT Hub. Puede crear esta directiva en hello [portal de Azure] [ lnk-management-portal] o mediante programación. servicio de token de Hello usa esta directiva toosign Hola símbolos (tokens) crea.
1. Cuando un dispositivo necesita tooaccess su centro de IoT, solicita un token firmado de su servicio de token. dispositivo de Hola puede autenticar con la identidad del dispositivo identidad personalizada del registro/autenticación esquema toodetermine Hola que el servicio de token de hello utiliza símbolo (token) de toocreate Hola.
1. servicio de token de Hello devuelve un token. Hello símbolo (token) se crea utilizando `/devices/{deviceId}` como `resourceURI`, con `deviceId` como dispositivo de Hola que se va a autenticar. servicio de token de Hello usa Hola acceso compartido directiva tooconstruct Hola símbolo (token).
1. dispositivo de Hello usa token Hola directamente con el centro de IoT Hola.

> [!NOTE]
> Puede utilizar la clase de .NET de hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] u Hola clase Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un token en el servicio de token.

servicio de token de Hello puede establecer caducidad del testigo Hola según sea necesario. Cuando expira el token de hello, centro de IoT Hola servidores de conexión del dispositivo Hola. A continuación, Hola debe solicitar un nuevo token de servicio de token de Hola. Una hora de expiración corto aumenta la carga de hello en dispositivo de Hola y el servicio de token de Hola.

Para un concentrador de tooyour tooconnect de dispositivo, deberá agregar también se toohello del registro de identidad de centro de IoT: aunque Hola dispositivo usa un token y no un tooconnect de clave de dispositivo. Por lo tanto, puede seguir el control de acceso por dispositivo toouse habilitando o deshabilitando las identidades del dispositivo en hello [del registro de identidad][lnk-identity-registry]. Este enfoque mitiga los riesgos de hello del uso de tokens con tiempos de expiración largos.

### <a name="comparison-with-a-custom-gateway"></a>Comparación con una puerta de enlace personalizada

modelo de servicio de token de Hello es Hola recomienda tooimplement forma un esquema de registro/autenticación de identidad personalizada con el centro de IoT. Este patrón se recomienda porque el centro de IoT sigue toohandle la mayor parte del tráfico de la solución de Hola. Sin embargo, si el esquema de autenticación personalizado de Hola por lo que es entrelazado con protocolo de hello, puede requerir un *puerta de enlace personalizado* tooprocess todos Hola tráfico. Un ejemplo de escenario de este tipo es la [seguridad de la capa de transporte (TLS) y las claves previamente compartidas (PSK)][lnk-tls-psk]. Para obtener más información, vea hello [puerta de enlace de protocolo] [ lnk-protocols] tema.

## <a name="reference-topics"></a>Temas de referencia:

Hello temas de referencia siguientes proporcionan más información sobre el centro de IoT de controlar acceso tooyour.

## <a name="iot-hub-permissions"></a>Permisos de IoT Hub

Hello tabla siguiente enumera los permisos de hello puede usar Centro de IoT de toocontrol acceso tooyour.

| Permiso | Notas |
| --- | --- |
| **RegistryRead**. |Registro de identidad de toohello de concede acceso de lectura. Para más información, consulte [Registro de identidad][lnk-identity-registry]. <br/>Este permiso se usa en servicios de back-end en la nube. |
| **RegistryReadWrite**. |Concede acceso de lectura y escritura toohello del registro de identidad. Para más información, consulte [Registro de identidad][lnk-identity-registry]. <br/>Este permiso se usa en servicios de back-end en la nube. |
| **ServiceConnect**. |Concede acceso toocloud orientada a servicios comunicación y supervisión de los puntos de conexión. <br/>Concede permiso tooreceive dispositivo a la nube mensajes, enviar mensajes en la nube al dispositivo y Hola recuperar correspondientes confirmaciones de entrega. <br/>Confirmaciones de entrega de tooretrieve concede permiso para el archivo de carga. <br/>Concede permiso tooaccess dispositivo: los gemelos tooupdate etiquetas y propiedades que desee, recuperar las propiedades de informes y ejecutar consultas. <br/>Este permiso se usa en servicios de back-end en la nube. |
| **DeviceConnect**. |Concede acceso a extremos de acceso toodevice. <br/>Concede permiso toosend dispositivo a la nube los mensajes y recibir mensajes en la nube al dispositivo. <br/>Concede permiso tooperform la carga de archivos desde un dispositivo. <br/>Concede permiso tooreceive gemelas deseado propiedad las notificaciones del dispositivo y el dispositivo de actualización de dos propiedades notificados. <br/>Carga el archivo tooperform de concesiones de permisos. <br/>Este permiso lo usan los dispositivos. |

## <a name="additional-reference-material"></a>Material de referencia adicional

Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* [Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* [Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola y comportamientos que se aplican toohello servicio del centro de IoT de limitación.
* [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* [Lenguaje de consulta de centro de IoT] [ lnk-query] describe el lenguaje de consulta de Hola que puede utilizar información tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.
* [Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toocontrol tener acceso a centro de IoT, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:

* [Usar el estado del dispositivo: los gemelos toosynchronize y configuraciones][lnk-devguide-device-twins]
* [Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola centro de IoT tutoriales:

* [Introducción a Azure IoT Hub][lnk-getstarted-tutorial]
* [Cómo mensajes toosend en la nube al dispositivo con el centro de IoT][lnk-c2d-tutorial]
* [¿Cómo tooprocess mensajes del dispositivo a la nube de centro de IoT][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
