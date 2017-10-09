---
title: "las conexiones híbridas de retransmisión aaaAzure protocolo guía | Documentos de Microsoft"
description: "Guía del protocolo de conexiones híbridas de Azure Relay."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Protocolo de conexiones híbridas de Azure Relay
Retransmisión de Azure es uno de los pilares de capacidad clave Hola de plataforma de Azure Service Bus Hola. Hola nueva *conexiones híbridas* capacidad de retransmisión es una evolución segura, protocolo abierto basada en HTTP y WebSockets. Sustituye primero hello, igualmente denominado *servicios de BizTalk* característica que se basa en un protocolo propietario. integración de Hola de conexiones híbridas en servicios de aplicaciones de Azure continuará toofunction como-es.

Conexiones híbridas permite establecer una comunicación de secuencias binaria y bidireccional entre dos aplicaciones en red durante la que una de las partes, o ambas, pueden residir detrás de firewalls o mecanismos NAT. Este artículo describen las interacciones de cliente de hello con retransmisión de conexiones híbridas de Hola para conectar los clientes en el agente de escucha y funciones de remitente, y cómo los agentes de escucha aceptan nuevas conexiones.

## Modelo de interacción
retransmisión de conexiones híbridas de Hello conecta dos partes proporcionando un punto de rendezvous Hola nube de Azure que ambas partes pueden detectar y conectarse toofrom perspectiva de su propia red. Ese punto de rendezvous se denomina "Conexión híbrida" en ésta y otra documentación en hello API y también en hello portal de Azure. Hello las conexiones híbridas de extremo de servicio conoce tooas Hola "servicio" para el resto de Hola de este artículo. modelo de interacción de Hola se basa en la nomenclatura de hello establecida por muchas otras API de red.

No hay un agente de escucha que primero indica las conexiones entrantes de preparación toohandle y acepta posteriormente cuanto llegan. En Hola otro lado, una conexión de cliente que se conecta hacia el agente de escucha de hello, se espera que toobe conexión aceptada para establecer una ruta de acceso de comunicación bidireccional.
"Conectar", "Escuchar" y "Aceptar" se Hola mismo términos que encontrará en la mayoría de API de socket.

Cualquier modelo de comunicación retransmitida tiene cualquiera de las partes que realiza las conexiones salientes a un extremo de servicio que realiza a escucha"hello" también un "cliente" en uso coloquiales y también puede provocar otras sobrecargas de terminología. terminología precisa Hello, por tanto, usamos para las conexiones híbridas es como sigue:

programas de Hello en ambos lados de una conexión se denominan a "clientes", ya que son servicio toohello de los clientes. cliente que espera y acepta conexiones es la "escucha", o es Hello dice toobe Hola "agente de escucha rol." cliente de Hola que inicia una nueva conexión a un agente de escucha a través del servicio de Hola se denomina "sender" hello, o está en la "función de remitente".

### Interacciones del agente de escucha
agente de escucha de Hello tiene cuatro interacciones con el servicio de hello; todos los detalles de conexión se describen más adelante en este artículo en la sección de referencia de Hola.

#### Escuchar
servicio de toohello de preparación de tooindicate que un agente de escucha está listo tooaccept conexiones, crea una conexión de WebSocket de salida. Protocolo de enlace de conexión de Hello lleva nombre Hola de una conexión híbrida configurado en el espacio de nombres de retransmisión de Hola y un token de seguridad que confiere Hola "Escucha" secundario en ese nombre.
Cuando se acepta hello WebSocket servicio hello, registro de hello está completado y Hola establecido web que websocket se mantiene activo como Hola "canal de control" para habilitar todas las interacciones subsiguientes. servicio de Hello permite too25 agentes de escucha simultáneos en una conexión híbrida. Si hay dos, o más, agentes de escucha activos, las conexiones entrantes se reparten entre ellos en orden aleatorio, por lo que no se garantiza que la distribución sea equitativa.

#### Accept
Cuando un remitente abre una nueva conexión de servicio de hello, servicio de hello elige y notifica a uno de los agentes de escucha activos de hello en hello conexión híbrida. Esta notificación se envía el agente de escucha de toohello a través del canal de control abierto de Hola como un mensaje JSON que contienen direcciones URL de Hola de punto de conexión de WebSocket de Hola Hola agente de escucha debe conectarse toofor acepte Hola conexión.

dirección URL de Hello puede y debe usarse directamente por el agente de escucha de hello sin ningún trabajo adicional.
información de Hello codificado es es sólo es válido durante un breve período de tiempo, básicamente para siempre como remitente de hello toowait dispuesto para hello conexión toobe establecido-to-end, pero la tooa máximo de 30 segundos. dirección URL de Hello sólo puede utilizarse para tratar de una conexión correcta. Tan pronto como hello WebSocket retransmite conexión con rendezvous de Hola que se establece la dirección URL, toda la actividad más este WebSocket y remitente toohello, sin intervención ni interpretación por servicio Hola.

#### Renovación
token de seguridad de Hola que debe ser el agente de escucha de tooregister usado hello y mantener que puede expirar el canal de control mientras el agente de escucha de hello está activo. caducidad del token Hello no afecta a las conexiones salientes, pero que se produzca toobe de canal de control de hello colocando el servicio de hello en o poco después de este momento Hola de expiración. operación de "renovar" Hello es un mensaje JSON que Hola agente de escucha puede enviar token de hello tooreplace asociado con el canal de control de hello, por lo que hello canal de control se puede mantener durante períodos prolongados.

#### Ping
Si el canal de control de hello permanece inactivo durante mucho tiempo, intermediarios en forma de hello, como cargar equilibradores o NAT pueden quitar conexión de TCP de Hola. operación de "ping" Hello evita tener que mediante el envío de una pequeña cantidad de datos en el canal de Hola que recuerda a todos los usuarios de la ruta de red de hello esa conexión Hola está pensado toobe activo, y también sirve como una prueba de "activa" para el agente de escucha de Hola. Si se produce un error de ping de hello, canal de control de hello debe considerarse inutilizable y debe volver a conectar el agente de escucha de Hola.

### Interacción del remitente
remitente de Hello solo tiene una sola interacción con el servicio de hello: se conecta.

#### Conectar
operación de "conectar" Hello abre un WebSocket en servicio de hello, proporcionar nombre de Hola de hello conexión híbrida y (si lo desea, pero es necesario de forma predeterminada) un token de seguridad conceder el permiso "Send" en la cadena de consulta de Hola. servicio Hello, a continuación, interactúa con el agente de escucha de Hola Hola forma descrita anteriormente, y el agente de escucha de hello crea una conexión de rendezvous que se une con este WebSocket. Una vez haya sido aceptado hello WebSocket, son todas las interacciones en ese WebSocket con un agente de escucha conectado.

### Resumen de interacción
resultado de Hello de este modelo de interacción es que el cliente remitente Hola haya salido el protocolo de enlace con un WebSocket "limpio", que es el agente de escucha de tooa conectado y que no es necesario más preámbulos o preparación. Este modelo permite prácticamente cualquier existente WebSocket cliente implementación tooreadily aprovechar las ventajas del programa Hola a servicio de conexiones híbridas proporcionando una dirección URL creada correctamente en su nivel de cliente de WebSocket.

conexión de encuentro de Hello WebSocket que Hola agente de escucha que se obtiene a través de la interacción de aceptación también está limpia y puede entregarse tooany implementación de servidor de WebSocket existente con una abstracción adicional mínima que distingue entre "Aceptar" operaciones en los agentes de escucha de red local y remoto de conexiones híbridas de su marco de trabajo "operaciones de aceptación".

## Referencia de protocolos

En esta sección se describe los detalles de Hola de interacciones de protocolo de Hola que se ha descrito anteriormente.

Todas las conexiones WebSocket se realizan en el puerto 443 como una actualización de la versión 1.1 de HTTPS, que normalmente la abstrae alguna API o marco de WebSocket. La descripción que ofrecemos en este documento sirve para cualquier tipo de implementación; no sugerimos ningún marco concreto.

### Protocolo del agente de escucha
Protocolo de agente de escucha de Hello consta de dos movimientos de conexión y tres operaciones de mensajes.

#### Conexión de canal de control del agente de escucha
canal de control de Hola se abre con la creación de una conexión de WebSocket para:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Hola `namespace-address` es Hola de nombre de dominio completo del espacio de nombres de retransmisión de Azure de Hola que hosts Hola conexión híbrida, normalmente de forma hello `{myname}.servicebus.windows.net`.

Opciones de parámetros de cadena de consulta de Hello son los siguientes.

| Parámetro | Obligatorio | Descripción |
| --- | --- | --- |
| `sb-hc-action` |Sí |Para Hola Hola de rol de agente de escucha parámetro debe ser **sb-hc-action = escucha** |
| `{path}` |Sí |ruta de acceso de espacio de nombres codificados de dirección URL de Hola de hello había preconfigurado conexión híbrida tooregister este agente de escucha en. Esta expresión es anexado toohello fijada `$hc/` parte de la ruta de acceso. |
| `sb-hc-token` |Sí\* |Hello agente de escucha debe proporcionar un válido, con codificación URL Service Bus compartido Token de acceso para el espacio de nombres de Hola o conexión híbrida que confiere hello **escuchar** derecho. |
| `sb-hc-id` |No |Este id. opcional especificado por el cliente permite realizar un seguimiento de diagnósticos completo. |

Si se produce un error en conexión de WebSocket de hello debido toohello ruta de acceso de conexión híbrida no está registrado, o un símbolo (token) no válido o ausente o algún otro error, se proporcionan comentarios de errores de Hola con modelo de comentarios de Hola regular HTTP 1.1 estado. La descripción del estado contiene un identificador de seguimiento de errores que se pueda comunicar al equipo de soporte técnico de Azure:

| Código | Error | Descripción |
| --- | --- | --- |
| 404 |No encontrado |ruta de acceso de conexión híbrida de Hello no es válido o dirección URL base de hello tiene un formato incorrecto. |
| 401 |No autorizado |token de seguridad de Hello es falta o tiene un formato incorrecto o no es válido. |
| 403 |Prohibido |token de seguridad de Hello no es válido para esta ruta de acceso para esta acción. |
| 500 |Error interno |Se produjo un error en el servicio de Hola. |

Si Hola conexión de WebSocket intencionadamente se cierra por servicio Hola después de haberse establecido inicialmente la razón de Hola para hacerlo, por lo que se comunica con un código de error de protocolo WebSocket adecuado junto con un mensaje de error descriptivo que también incluye un seguimiento ID. servicio de Hello no se apagará el canal de control sin que se produzca una condición de error. Todos los cierres "limpios" los controla el cliente.

| Estado de WS | Descripción |
| --- | --- |
| 1001 |ruta de acceso de conexión híbrida de Hola se ha eliminado o deshabilitado. |
| 1008 |expiró el token de seguridad de Hello, por lo tanto, se infringe la directiva de autorización de Hola. |
| 1011 |Se produjo un error en el servicio de Hola. |

### Protocolo de enlace de aceptación
Hola "Aceptar" notificación se envía por el agente de escucha de hello servicio toohello a través del canal de control establecida previamente como un mensaje JSON en un marco de texto de WebSocket. No hay ningún mensaje de respuesta de toothis.

mensaje de bienvenida contiene un objeto JSON con el nombre "Aceptar", que define Hola propiedades siguientes en este momento:

* **dirección** : Hola toobe de cadena de dirección URL utilizada para establecer hello WebSocket toothe servicio tooaccept una conexión entrante.
* **Id. de** : Hola identificador único para esta conexión. Si se proporcionó ningún identificador hello cliente remitente de hello, es el valor de remitente proporcionado de hello, en caso contrario, es un valor generado por el sistema.
* **connectHeaders** : todos los encabezados HTTP que se han proporcionado el extremo de retransmisión toohello remitente hello, que también incluye Hola protocolo de WebSocket de segundo y los encabezados de extensiones de WebSocket de segundo.

#### Mensaje accept

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Hola dirección URL proporcionada en hello mensaje JSON se usa por el agente de escucha de Hola para establecer Hola WebSocket para aceptar o rechazar el socket de remitente de Hola.

#### Aceptar Hola socket
tooaccept, el agente de escucha de hello establece una dirección de toohello proporcionado de conexión de WebSocket.

Si hello "Aceptar" mensaje realiza una `Sec-WebSocket-Protocol` encabezado, se espera ese agente de escucha de hello solo acepta hello WebSocket si admite dicho protocolo. Además, Establece el encabezado de hello como hello que websocket se ha establecido.

Hello Esto mismo aplica toohello `Sec-WebSocket-Extensions` encabezado. Si el marco de trabajo de hello es compatible con una extensión, se debe establecer respuesta de servidor de hello encabezado toohello de hello necesario `Sec-WebSocket-Extensions` protocolo de enlace para la extensión de Hola.

dirección URL de Hello debe usarse como-es para establecer Hola aceptan socket, pero contiene los parámetros siguientes:

| Parámetro | Obligatorio | Descripción |
| --- | --- | --- |
| `sb-hc-action` |Sí |Para aceptar un socket, debe ser el parámetro hello`sb-hc-action=accept` |
| `{path}` |Sí |(vea Hola después de párrafo) |
| `sb-hc-id` |No |Consulte la descripción anterior del **identificador**. |

`{path}`es la ruta de acceso de espacio de nombres codificados de dirección URL de Hola de hello preconfigurado conexión híbrida en qué tooregister este agente de escucha. Esta expresión es anexado toothe fijada `$hc/` parte de la ruta de acceso. 

Hola `path` expresión puede ampliarse con un sufijo y una expresión de cadena de consulta que sigue el nombre registrado Hola después de una barra diagonal separar. Esto permite a Hola remitente toopass envío argumentos toohello aceptación escucha de cliente cuando no es posible tooinclude HTTP encabezados. es ese agente de escucha de hello framework redistribuye parte de la ruta de acceso fija de Hola y Hola nombre registrado de la ruta de acceso Hello expectativa y hace que el resto de hello, posiblemente sin ningún argumento de cadena de consulta precedida por `sb-`, aplicación toohello disponible para decidir si tooaccept Hola conexión.

Para obtener más información, vea Hola pasos de la sección "Protocolo de remitente".

Si hay un error, el servicio de hello puede responder como sigue:

| Código | Error | Descripción |
| --- | --- | --- |
| 403 |Prohibido |Hola URL no es válida. |
| 500 |Error interno |Se produjo un error en el servicio de Hola |

Una vez establecida la conexión de hello, servidor de hello apaga hello WebSocket cuando remitente hello WebSocket apaga, o con hello siguiente estado:

| Estado de WS | Descripción |
| --- | --- |
| 1001 |cliente de remitente de Hello apaga conexión Hola. |
| 1001 |ruta de acceso de conexión híbrida de Hola se ha eliminado o deshabilitado. |
| 1008 |expiró el token de seguridad de Hello, por lo tanto, se infringe la directiva de autorización de Hola. |
| 1011 |Se produjo un error en el servicio de Hola. |

#### Rechazar el socket de Hola
Rechazar socket Hola después de Inspeccionar mensaje de Hola "Aceptar" requiere un protocolo de enlace similar hello código de estado y descripción del estado de comunicación que puede fluir la razón del rechazo de Hola de nuevo toohello remitente.

opción de diseño de protocolo de Hello aquí es toouse un protocolo de enlace de WebSocket (es decir, tooend diseñada en un estado de error definida) para que las implementaciones de cliente de agente de escucha pueden continuar toorely en un cliente de WebSocket y no es necesario emplear adicional, el cliente HTTP.

socket de tooreject Hola, cliente hello toma Hola dirección URI del mensaje de "Aceptar" hello y anexa dos tooit de parámetros de cadena de consulta, como se indica a continuación:

| Parámetro | Obligatorio | Descripción |
| --- | --- | --- |
| statusCode |yes |Código de estado HTTP numérico. |
| statusDescription |Sí |Motivo legible humano de rechazo de Hola. |

Hola que URI resultante es, a continuación, utiliza una conexión de WebSocket tooestablish.

Cuando se completa correctamente, este protocolo de enlace genera un error de forma intencionada con el código HTTP 410, ya que no se ha establecido ningún WebSocket. Si algo va mal, describe los Hola siguientes códigos de error hello:

| Código | Error | Descripción |
| --- | --- | --- |
| 403 |Prohibido |Hola URL no es válida. |
| 500 |Error interno |Se produjo un error en el servicio de Hola. |

### Renovación del token del agente de escucha
Cuando está en el token de agente de escucha de hello sobre tooexpire, puede reemplazar mediante el envío de un servicio de toohello de mensaje de texto marco a través del canal de control de hello establecida. El mensaje contiene un objeto JSON denominado `renewToken`, que define Hola después de propiedad en este momento:

* **símbolo (token)** : un token de acceso compartido de Bus de servicio válido, codificados de dirección URL para el espacio de nombres o la conexión híbrida que confiere hello **escuchar** derecho.

#### Mensaje renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Si se produce un error en la validación del token hello, se deniega el acceso y servicio de nube de hello cierra el canal de control de hello WebSocket con un error. En caso contrario, no se produce ninguna respuesta.

| Estado de WS | Descripción |
| --- | --- |
| 1008 |expiró el token de seguridad de Hello, por lo tanto, se infringe la directiva de autorización de Hola. |

## Protocolo del remitente
Protocolo del remitente de Hello es un agente de escucha se establece de forma de toohello idéntico.
objetivo de Hello es la máxima transparencia para to-end hello WebSocket. dirección de Hello conectar hello toois que mismas que para el agente de escucha de hello, pero la acción"hello" es diferente y el token tiene un permiso diferente:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Hola *dirección de espacio de nombres* es Hola de nombre de dominio completo del espacio de nombres de retransmisión de Azure de Hola que hosts Hola conexión híbrida, normalmente de forma hello `{myname}.servicebus.windows.net`.

solicitud de Hello puede contener arbitrarios encabezados HTTP adicionales, incluso los definidos por la aplicación. Todos los proporciona el agente de escucha de encabezados flujo toohello y pueden encontrarse en hello `connectHeader` objeto de hello **Aceptar** mensaje de control.

Opciones de parámetros de cadena de consulta de Hello son los siguientes:

| Parámetro | ¿Necesario? | Descripción |
| --- | --- | --- |
| `sb-hc-action` |Sí |Para la función de remitente de hello, debe ser el parámetro hello `action=connect`. |
| `{path}` |Sí |(vea Hola después de párrafo) |
| `sb-hc-token` |Sí\* |Hello agente de escucha debe proporcionar un válido, con codificación URL Service Bus compartido Token de acceso para el espacio de nombres de Hola o conexión híbrida que confiere hello **enviar** derecho. |
| `sb-hc-id` |No |Un identificador opcional que permite el seguimiento de diagnóstico-to-end y se realiza el agente de escucha de toohello disponible durante Hola acepta el protocolo de enlace. |

Hola `{path}` es la ruta de acceso de espacio de nombres codificados de dirección URL de Hola de hello preconfigurado conexión híbrida en qué tooregister este agente de escucha. Hola `path` expresión puede ampliarse con un sufijo y aún más una toocommunicate de expresión de cadena de consulta. Si se ha registrado en la ruta de acceso de Hola Hola conexión híbrida `hyco`, hello `path` expresión puede ser `hyco/suffix?param=value&...` seguido por parámetros de cadena de consulta de hello definidas aquí. Una expresión completa puede ser como la siguiente:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Hola `path` expresión se pasa a través de agente de escucha de toohello en dirección Hola URI incluido en el mensaje de control de Hola "Aceptar".

Si se produce un error en hello conexión de WebSocket de vencimiento toohello ruta de acceso de conexión híbrida no está registrado, un símbolo (token) no válido o ausente o algún otro error, se proporcionan comentarios de errores de hello con modelo de comentarios de Hola regular HTTP 1.1 estado. La descripción del estado contiene un identificador de seguimiento de errores que se pueda comunicar al equipo de soporte técnico de Azure:

| Código | Error | Descripción |
| --- | --- | --- |
| 404 |No encontrado |ruta de acceso de conexión híbrida de Hello no es válido o dirección URL base de hello tiene un formato incorrecto. |
| 401 |No autorizado |token de seguridad de Hello es falta o tiene un formato incorrecto o no es válido. |
| 403 |Prohibido |token de seguridad de Hello no es válido para esta ruta de acceso y de esta acción. |
| 500 |Error interno |Se produjo un error en el servicio de Hola. |

Si Hola conexión de WebSocket se cierra intencionadamente por servicio de hello después de que se ha establecido inicialmente, razón de Hola para hacerlo por lo que se comunica con un código de error de protocolo WebSocket adecuado junto con un mensaje de error descriptivo que también incluye un Id. de seguimiento.

| Estado de WS | Descripción |
| --- | --- |
| 1000 |agente de escucha de Hello apaga socket Hola. |
| 1001 |ruta de acceso de conexión híbrida de Hola se ha eliminado o deshabilitado. |
| 1008 |expiró el token de seguridad de Hello, por lo tanto, se infringe la directiva de autorización de Hola. |
| 1011 |Se produjo un error en el servicio de Hola. |

## Pasos siguientes
* [Preguntas más frecuentes acerca de Relay](relay-faq.md)
* [Creación de un espacio de nombres](relay-create-namespace-portal.md)
* [Introducción a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introducción a Node](relay-hybrid-connections-node-get-started.md)

