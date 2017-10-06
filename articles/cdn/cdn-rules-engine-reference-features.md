---
title: "características del motor de reglas de aaaAzure CDN | Documentos de Microsoft"
description: "Documentación de referencia sobre las condiciones y características de coincidencia del motor de reglas de la red CDN de Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Características del motor de reglas de la red CDN de Azure
Este tema enumeran las descripciones detalladas de las características disponibles de hello del red de entrega de contenido (CDN) para Azure [motor de reglas de](cdn-rules-engine.md).

Hola tercera parte de una regla es característica Hola. Una característica define el tipo de saludo de acción que será aplicado toohello tipo de solicitud que se identifica mediante un conjunto de condiciones de coincidencia.

## <a name="access"></a>Access

Estas características están diseñadas toocontrol acceso toocontent.


Nombre | Propósito
-----|--------
Denegar acceso | Determina si todas las solicitudes se rechazan con una respuesta 403-Prohibido.
Autenticación de token | Determina si la autenticación basada en Token serán solicitud tooa aplicada.
Código de denegación de autorización de token | Determina el tipo de saludo de respuesta que se devolverán tooa usuario cuando se deniegue una solicitud debido a la autenticación tooToken.
Ignorar mayúsculas y minúsculas en URL de autenticación de token | Determina si las comparaciones de URL realizadas por la autenticación basada en tokens distinguirán mayúsculas de minúsculas.
Parámetro de autenticación de token | Determina si se debe cambiar el nombre de parámetro de cadena de consulta de autenticación basada en autorización Token de Hola.

### <a name="deny-access"></a>Denegar acceso
**Propósito**: determina si todas las solicitudes se rechazan con una respuesta 403 Prohibido.

Valor | Resultado
------|-------
habilitado| Hace que todas las solicitudes que cumplen toobe Hola de criterios coincidentes rechazado con respuesta 403 Prohibido.
Disabled| Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es tooallow Hola origen server toodetermine Hola tipo de respuesta que se devolverá.

**Comportamiento predeterminado**: deshabilitado.

> [!TIP]
   > Un uso posible para esta característica es tooassociate con un encabezado de solicitud coincide con la condición tooblock acceso tooHTTP sitios de referencia que están usando el contenido de tooyour vínculos alineado.

### <a name="token-auth"></a>Autenticación de token
**Propósito:** determina si la autenticación basada en Token serán solicitud tooa aplicada.

Si está habilitada la autenticación basada en el símbolo (token), se cumplirán sólo las solicitudes que proporcionan un token cifrado y cumplan los requisitos de toohello especificados por ese token.

clave de cifrado de Hola que será utilizados valores de símbolo (token) tooencrypt y descifrar viene determinado por la clave principal y las opciones de clave de copia de seguridad en la página de autenticación de Token. Tenga en cuenta que las claves de cifrado son específicas de la plataforma.

Valor | Resultado
------|---------
habilitado | Protege Hola solicita contenido con autenticación basada en el símbolo (token). Solo se admitirán las solicitudes de los clientes que proporcionen un token válido y cumplan los requisitos. Las transacciones de FTP se excluyen de la autenticación basada en token.
Disabled| Restaura el comportamiento predeterminado de Hola. Hola comportamiento predeterminado es tooallow su toodetermine de configuración de autenticación basada en el símbolo (token) si una solicitud que se va a proteger.

**Comportamiento predeterminado**: deshabilitado.

###<a name="token-auth-denial-code"></a>Código de denegación de autorización de token
**Propósito:** determina el tipo de Hola de respuesta que se devolverán tooa usuario cuando se deniegue una solicitud debido a la autenticación tooToken.

códigos de respuesta disponibles de Hola se enumeran a continuación.

Código de respuesta|Nombre de la respuesta|Descripción
----------------|-----------|--------
301|Movido permanentemente|Este código de estado redirige los usuarios no autorizados toohello URL especificado en el encabezado de ubicación.
302|Encontrado|Este código de estado redirige los usuarios no autorizados toohello URL especificado en el encabezado de ubicación. Este código de estado es el método estándar del sector Hola de llevar a cabo una redirección.
307|Redirección temporal|Este código de estado redirige los usuarios no autorizados toohello URL especificado en el encabezado de ubicación.
401|No autorizado|La combinación de este código de estado con el encabezado de respuesta WWW-Authenticate permite tooprompt un usuario para la autenticación.
403|Prohibido|Se trata de hello estándar 403 Prohibido mensaje de estado que un usuario no autorizado verán cuando intente tooaccess contenido protegido.
404|Archivo no encontrado|Este código de estado indica que cliente HTTP de hello fue capaz de toocommunicate con el servidor de hello, pero Hola solicitado no se encontró el contenido.

#### <a name="url-redirection"></a>Redirección de URL

Esta característica admite tooa definido por el usuario URL de redirección de dirección URL cuando esté configurado tooreturn un código de estado 3xx. Esta dirección URL definida por el usuario puede especificarse mediante la realización de hello pasos:

1. Seleccionar un código de respuesta de 3xx para la característica de código de denegación de autorización Token de Hola.
2. Seleccione "Location" en la opción Optional Header Name (Nombre de encabezado opcional).
3. Establecer la dirección URL toohello deseado de opción de valor de encabezado opcional.

Si una dirección URL no está definida para un código de estado 3xx, hello página de respuesta estándar para un código de estado 3xx se devolverán toohello usuario.

La redirección de URL solo es aplicable a los códigos de respuesta 3xx.

La opción Optional Header Value (Valor de encabezado opcional) admite caracteres alfanuméricos, comillas y espacios.

#### <a name="authentication"></a>Autenticación

Esta característica admite el encabezado de hello capacidad tooinclude el WWW-Authenticate al responder tooan solicitud no autorizada para el contenido protegido por autenticación basada en Token. Si se ha establecido el encabezado WWW-Authenticate demasiado "básico" en la configuración, un usuario no autorizado Hola le pedirá las credenciales de cuenta.

Hola por encima de la configuración puede lograrse mediante la realización de hello pasos:

1. Seleccione "401" como código de respuesta de hello de la característica de código de denegación de autorización Token de Hola.
2. Seleccione "WWW-Authenticate" en la opción Optional Header Name (Nombre de encabezado opcional).
3. Establecer la opción de valor de encabezado opcional demasiado "básica".

El encabezado WWW-Authenticate solo es aplicable a códigos de respuesta 401.

### <a name="token-auth-ignore-url-case"></a>Ignorar mayúsculas y minúsculas en URL de autenticación de token
**Propósito**: determina si las comparaciones de URL realizadas por la autenticación basada en token distinguirán mayúsculas de minúsculas.

parámetros de Hello afectadas por esta característica son:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Los valores válidos son:

Valor|Resultado
---|----
habilitado|Hace que el servidor perimetral tooignore caso al comparar las direcciones URL para los parámetros de autenticación basada en el símbolo (token).
Disabled|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es para las comparaciones de dirección URL para la autenticación de Token toobe entre mayúsculas y minúsculas.

**Comportamiento predeterminado**: deshabilitado.
 
### <a name="token-auth-parameter"></a>Parámetro de autenticación de token
**Propósito:** determina si se debe cambiar el nombre de parámetro de cadena de consulta de autenticación basada en autorización Token de Hola.

Información importante:

- La opción de valor define a través del cual se puede especificar un token de nombre del parámetro de cadena de consulta Hola.
- No se puede establecer la opción de valor demasiado "ec_token."
- Asegúrese de que ese nombre hello definido en la opción de valor solo 
- contenga caracteres de dirección URL válidos.

Valor|Resultado
----|----
habilitado|La opción de valor define a través del cual se deberían definir los tokens de nombre del parámetro de cadena de consulta Hola.
Disabled|Un token se puede especificar como un parámetro de cadena de consulta no definido en la dirección URL de solicitud de saludo.

**Comportamiento predeterminado**: deshabilitado. Un token se puede especificar como un parámetro de cadena de consulta no definido en la dirección URL de solicitud de saludo.

## <a name="caching"></a>Almacenamiento en caché

Estas características están diseñada toocustomize y cuándo y cómo se almacena en caché el contenido.

Nombre | Propósito
-----|--------
Parámetros de ancho de banda | Determina si se activarán los parámetros de limitación de ancho de banda (es decir, ec_rate y ec_prebuf).
Limitación de ancho de banda | Limita el ancho de banda de Hola de respuesta de hello proporcionada por nuestros servidores de borde.
Omisión de la memoria caché | Determina si la solicitud de hello puede aprovechar nuestra tecnología de almacenamiento en caché.
Tratamiento de encabezado Cache-Control | Controles Hola generación de encabezados de Cache-Control de servidor de hello borde cuando está activa la característica externa Max-Age.
Cadena de consulta de clave de caché | Determina si Hola de clave de caché se incluir o excluir los parámetros de cadena de consulta asociados a una solicitud.
Reescritura de clave de caché | Reescribe asociada a una solicitud de clave de caché Hola.
Relleno de la memoria caché completa | Determina lo que ocurre cuando una solicitud tiene como resultado un error de caché parcial en un servidor perimetral.
Comprimir tipos de archivo | Define los formatos de archivo de Hola que se va a comprimir en el servidor de Hola.
Max-Age interna predeterminada | Determina intervalo de max-age predeterminado de hello para la revalidación de la caché de servidor de borde server tooorigin.
Tratamiento del encabezado Expires | Controles Hola generación de encabezados Expires por un servidor perimetral cuando Hola externo Max-Age característica está activa.
Max-Age externa | Determina el intervalo de duración máxima de Hola de revalidación de la caché de explorador tooedge server.
Forzar Max-Age interna | Determina el intervalo de max-age de hello para la revalidación de la caché de servidor de borde server tooorigin.
Compatibilidad de H.264 (Descarga progresiva de HTTP) | Determina los tipos de Hola de H.264 formatos de archivo que pueden ser usado toostream contenido.
Respetar solicitud de no almacenar en caché | Determina si las solicitudes de no almacenar en caché de un cliente HTTP se reenviarán toohello del servidor de origen.
Ignorar no almacenar en caché de origen | Determina si la CDN omitirá determinadas directivas procedentes de un servidor de origen.
Ignorar intervalos que no se puedan satisfacer | Determina la respuesta de Hola que se devolverán tooclients cuando una solicitud genera un código de estado 416 intervalo no se puede satisfacer solicitado.
Max-Stale interna | Controla cuánto tiempo han superado el tiempo de expiración normal de hello puede proporcionarse un recurso almacenado en caché desde un servidor perimetral cuando hello borde servidor toorevalidate no se puede Hola activo en caché con el servidor de origen de Hola.
Uso compartido de caché parcial | Determina si una solicitud puede generar contenido almacenado parcialmente en caché.
PreValidate contenido en caché | Determina si el contenido almacenado en caché será apto para la revalidación temprana antes de que expire su período de vida.
Actualizar archivos de caché de cero bytes | Determina cómo nuestros servidores perimetrales controlan la solicitud de un cliente HTTP para un recurso de la caché de 0 bytes.
Establecer códigos de estado almacenables en caché | Define el conjunto de Hola de códigos de estado que puede dar lugar a contenido almacenado en caché.
Entrega de contenido obsoleto en caso de error | Determina si expirado contenido almacenado en caché se entregará cuando se produce un error durante la revalidación de caché o cuando Hola recuperar solicita contenido desde el servidor de origen del cliente de Hola.
Obsoleto durante revalidación | Mejora el rendimiento al permitir que a nuestros servidores perimetrales solicitante de tooserve cliente obsoleto toohello mientras revalidación lleva a cabo.
Comentario | característica de comentario de Hello permite un toobe tenga en cuenta que se agregan dentro de una regla.

###<a name="bandwidth-parameters"></a>Parámetros de ancho de banda
**Propósito**: determina si se activarán los parámetros de limitación de ancho de banda (es decir, ec_rate y ec_prebuf).

Parámetros de limitación de ancho de banda determinan si Hola velocidad de transferencia de datos para la solicitud del cliente será tasa personalizado tooa limitado.

Valor|Resultado
--|--
habilitado|Permite que nuestros servidores perimetrales solicitudes de límite de ancho de banda de toohonor.
Disabled|Hace que nuestros servidores perimetrales parámetros de limitación de ancho de banda de tooignore. Hola solicita contenido se servirá normalmente (es decir, sin límite de ancho de banda).

**Comportamiento predeterminado**: habilitado.

###<a name="bandwidth-throttling"></a>Limitación de ancho de banda
**Propósito:** aceleradores Hola ancho de banda para la respuesta de hello proporcionada por nuestros servidores de borde.

Las siguientes opciones de Hola deben ser definida tooproperly configurar la limitación de ancho de banda.

Opción|Descripción
--|--
Kbytes por segundo|Establezca esta opción toohello ancho de banda máximo (Kb por segundo) que puede ser utilizados toodeliver Hola respuesta.
Segundos de búfer previo|Establece un número de segundos que nuestros servidores perimetrales esperará hasta que la limitación de ancho de banda toohello opción. Hola de este período de tiempo de ancho de banda no restringido sirve tooprevent un reproductor multimedia de experimenta entrecortado o problemas debido a la limitación de toobandwidth el almacenamiento en búfer.

**Comportamiento predeterminado**: deshabilitado.

###<a name="bypass-cache"></a>Omisión de la memoria caché
**Propósito:** determina si la solicitud de hello puede aprovechar nuestra tecnología de almacenamiento en caché.

Valor|Resultado
--|--
habilitado|Hace que todos los toofall las solicitudes a través del servidor de origen toohello, incluso si anteriormente se almacenó en caché contenido de hello en servidores perimetrales.
Disabled|Hace que los servidores de borde activos toocache según la directiva de caché toohello definida en sus encabezados de respuesta.

**Comportamiento predeterminado**:

- **HTTP grande:** deshabilitado

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Tratamiento de encabezados Cache-Control
**Propósito:** controla la generación Hola de encabezados de Cache-Control de servidor perimetral de hello cuando está activa la función Max-Age externa.

Hola tooachieve de manera más fácil este tipo de configuración es tooplace Hola Max-Age externo y las características de tratamiento de encabezado Cache-Control hello en Hola la misma instrucción.

Valor|Resultado
--|--
Sobrescribir|Se garantiza que Hola siguientes acciones llevará a cabo:<br/> -Sobrescribe el encabezado Cache-Control generado por el servidor de origen de Hola. <br/>: Agrega el encabezado Cache-Control generado por hello respuesta de toohello característica externa Max-Age.
Pass Through|Se asegura de que el encabezado Cache-Control generado por la característica de hello externo Max-Age nunca se ha agregado toohello respuesta. <br/> Si el servidor de origen de hello genera un encabezado Cache-Control, pasará a través de toohello por el usuario final. <br/> Si el servidor de origen de hello no genera un encabezado Cache-Control y, a continuación, esta opción puede contener un encabezado Cache-Control toonot de encabezado de respuesta de hello causa.
Add if Missing|Si no se recibió un encabezado Cache-Control de servidor de origen de hello, esta opción agrega el encabezado Cache-Control generado por la característica de hello externo Max-Age. Esta opción es útil para garantizar que todos los recursos se asignarán a un encabezado Cache-Control.
Remove| Esta opción garantiza que no se incluye con la respuesta de encabezado de hello un encabezado Cache-Control. Si ya se ha asignado un encabezado Cache-Control, se quitarán de la respuesta de encabezado de Hola.

**Comportamiento predeterminado**: sobrescribir.

###<a name="cache-key-query-string"></a>Cadena de consulta de clave de caché
**Propósito**: determina si la clave de caché incluirá o excluirá los parámetros de cadena de consulta asociados a una solicitud.

Información importante:

- Especifique uno o más nombres de parámetro de cadena de consulta. Cada nombre de parámetro debe delimitarse con un único espacio.
- Esta característica determina si los parámetros de cadena de consulta se pueden incluir o excluir de clave de caché de Hola. A continuación se proporciona información adicional para cada opción.

Tipo|Descripción
--|--
 Include|  Indica que cada parámetro especificado debe estar incluido en la clave de caché de Hola. Se generará una clave de caché única para cada solicitud que contenga un valor único para un parámetro de cadena de consulta definido en esta característica. 
 Include All  |Indica que se creará una clave de caché única para cada recurso de tooan de solicitud que incluye una cadena de consulta única. Este tipo de configuración no se recomienda normalmente puesto que puede provocar tooa pequeño porcentaje de aciertos de caché. Esto aumentará la carga de hello en el servidor de origen de hello, ya que tendrá tooserve más solicitudes. Esta configuración duplica Hola comportamiento conocido como "único-cache" en la página de almacenamiento en memoria caché en la cadena de consulta el almacenamiento en caché. 
 Exclude | Indica que solo Hola especifica parámetros se excluirán de la clave de caché de Hola. Todos los demás parámetros de cadena de consulta se incluirán en la clave de caché de Hola. 
 Exclude All  |Indica que todos los parámetros de cadena de consulta se excluirán de la clave de caché de Hola. Esta configuración duplica predeterminado Hola comportamiento, que se conoce como "standard-cache" en la página de almacenamiento en memoria caché en la cadena de consulta el almacenamiento en caché. 

potencia de Hola de motor de reglas de HTTP permite toocustomize manera de hello en el que se implementa el almacenamiento en caché de cadena de consulta. Por ejemplo, puede especificar que el almacenamiento en caché de cadena consultas solo se realizará en determinadas ubicaciones o tipos de archivo.

Si desea que la cadena de consulta de hello tooduplicate comportamiento conocido como "no-cache" en la página de almacenamiento en memoria caché en la cadena de consulta el almacenamiento en caché, deberá toocreate una regla que contiene una condición de coincidencia de caracteres comodín de consulta de dirección URL y una característica de caché de omisión. Hola condición de coincidencia de caracteres comodín de consulta de dirección URL se debe establecer tooan asterisco (*).

#### <a name="sample-scenarios"></a>Escenarios de ejemplo

El siguiente es ejemplo de uso de esta característica. Un ejemplo de solicitud y Hola predeterminados de clave de caché se proporcionan a continuación.

- **Solicitud de ejemplo:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&amp;language=EN&amp;userid=01
- **Clave de caché predeterminada:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Include

Configuración de ejemplo:

- **Tipo:** Include
- **Parámetros:** idioma

Este tipo de configuración generaría Hola después parámetro caché-clave de cadena de consulta:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Include All

Configuración de ejemplo:

- **Tipo:** Include All

Este tipo de configuración generaría Hola después parámetro caché-clave de cadena de consulta:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Exclude

Configuración de ejemplo:

- **Tipo:** Exclude
- **Parámetros:** id_sesión id_usuario

Este tipo de configuración generaría Hola después parámetro caché-clave de cadena de consulta:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Exclude All

Configuración de ejemplo:

- **Tipo:** Exclude All

Este tipo de configuración generaría Hola después parámetro caché-clave de cadena de consulta:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Reescritura de clave de caché
**Propósito:** reescribe Hola asociada a una solicitud de clave de caché.

Una clave de caché es Hola ruta de acceso relativa que identifica un recurso para fines de Hola de almacenamiento en caché. En otras palabras, nuestros servidores buscará una versión almacenada en caché de un recurso según la ruta de acceso de tooits tal como se define por su clave de caché.

Configurar esta característica mediante la definición de hello siguientes opciones:

Opción|Descripción
--|--
Ruta de acceso original| Definir tipos de toohello de ruta de acceso relativa de Hola de solicitudes se reescribirán cuya clave de caché. Para definir una ruta de acceso relativa, seleccione una ruta de acceso de origen de base y, a continuación, define un patrón de expresión regular.
Nueva ruta de acceso|Definir la ruta de acceso relativa de hello para la clave de caché nuevo Hola. Para definir una ruta de acceso relativa, seleccione una ruta de acceso de origen de base y, a continuación, define un patrón de expresión regular. Esta ruta de acceso relativa se puede construir dinámicamente mediante el uso de Hola de variables de tipo HTTP
**Comportamiento predeterminado:** de clave de una solicitud de caché viene determinada por el URI de solicitud de saludo.

###<a name="complete-cache-fill"></a>Relleno de la memoria caché completa
**Propósito**: determina lo que ocurre cuando una solicitud tiene como resultado un error de caché parcial en un servidor perimetral.

Un error de caché parcial describe el estado de la caché de Hola para un activo que no era el servidor perimetral de tooan descargado por completo. Si un recurso solo parcialmente se almacena en caché en un servidor perimetral, a continuación, hello solicitud siguiente para ese recurso se reenviarán nuevo toohello del servidor de origen.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Un error de caché parcial normalmente se produce después de que un usuario anule una descarga o en el caso de los recursos que se solicitan únicamente con solicitudes de intervalos HTTP. Esta característica es muy útil para recursos de gran tamaño donde los usuarios no suelen descargarán desde Inicio toofinish (p. ej., vídeos). Como resultado, esta característica está habilitada de forma predeterminada en la plataforma HTTP grandes Hola. Está deshabilitada en todas las demás plataformas.

Configuración de tooleave Hola predeterminada para la plataforma HTTP grandes de hello, se recomienda desde que se reduzca la carga de hello en el servidor de origen del cliente y aumentar la velocidad de hello en el que los clientes descargar su contenido.

Pagar toohello manera en la memoria caché de configuración se realiza un seguimiento, esta característica no se puede asociar con hello siguiendo las condiciones de coincidencia: borde Cname, Literal de encabezado de solicitud, comodín del encabezado de solicitud, el Literal de consulta de dirección URL y comodín de la consulta de dirección URL.

Valor|Resultado
--|--
habilitado|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es tooforce hello borde server tooinitiate una captura de fondo del activo de Hola desde el servidor de origen de Hola. Transcurrido ese período, estará activo hello en caché local del servidor de hello borde.
Disabled|Impide que un servidor perimetral realizar una captura de fondo de los activos de Hola. Esto significa que esa solicitud siguiente Hola de ese activo a partir de esa región hará que un toorequest de servidor perimetral del servidor de origen del cliente de Hola.

**Comportamiento predeterminado**: habilitado.

###<a name="compress-file-types"></a>Comprimir tipos de archivo
**Propósito:** define los formatos de archivo de Hola que se va a comprimir en el servidor de Hola.

Los formatos de archivo se pueden especificar con su tipo de medio de Internet (es decir, Content-Type). Tipo de medio de Internet es metadatos independiente de la plataforma que permite el formato de archivo de servidores tooidentify Hola de un determinado activo. La siguiente es la lista de los tipos de medios más comunes de Internet.

Tipo de medio de Internet|Descripción
--|--
text/plain|Texto sin formato
text/html| Archivos HTML
text/css|Hojas de estilos en cascada (CSS)
application/x-javascript|Javascript
application/javascript|Javascript
Información importante:

- Especifique varios tipos de medios de Internet delimitando cada uno con un solo espacio. 
- Esta característica solo comprimirá recursos con un tamaño inferior a 1 MB. Nuestros servidores no comprimirán los recursos de mayor tamaño.
- Algunos tipos de contenido, como las imágenes, los vídeos y los medios de audio (p. ej., JPG, MP3, MP4, etc.), ya están comprimidos. Una compresión adicional en estos tipos de recursos no reducirá significativamente el tamaño de archivo. Por lo tanto, se recomienda no habilitar la compresión en estos tipos de recursos.
- No se admiten caracteres comodín, como asteriscos.
- Antes de agregar esta regla de tooa de característica, asegúrese de tooset seguro de la opción de compresión deshabilitado en la página de compresión de hello plataforma toowhich que se aplicará esta regla.

###<a name="default-internal-max-age"></a>Max-Age interna predeterminada
**Propósito:** intervalo de max-age determina Hola predeterminado para la revalidación de la caché de servidor de borde server tooorigin. Cantidad de tiempo que transcurrirá antes de que un servidor perimetral comprobará si un recurso almacenado en caché coincide con asset Hola almacenado en el servidor de origen de Hola se hello en otras palabras.

Información importante:

- Esta acción solo se realizará para las respuestas de un servidor de origen que no asignen una indicación de max-age en el encabezado Cache-Control o Expires.
- Esta acción no se realizará para los recursos que no se consideran almacenables en caché.
- Esta acción no afecta a las nuevas validaciones de caché del servidor de tooedge de explorador. Estos tipos de nuevas validaciones vienen determinados por el encabezado Cache-Control o Expires encabezados enviaron toohello explorador, que se puede personalizar con la característica de Max-Age externo.
- resultados de Hola de esta acción no tiene un efecto notable en los encabezados de respuesta de Hola y el contenido de hello procedentes de servidores de borde para el contenido, pero puede tener un efecto en la cantidad de Hola de revalidación el tráfico enviado desde el servidor de origen de tooyour de servidores de borde.
- Para configurar esta característica:
    - Seleccionar el código de estado de hello para el que se puede aplicar un interno predeterminado max-age.
    - Especificar un valor entero y, a continuación, seleccionar Hola unidad de tiempo que desee (por ejemplo, segundos, minutos, horas, etcetera). Este valor define el intervalo de saludo predeterminado interno max-age.

- Unidad de tiempo de configuración Hola demasiado "Off" asignará un intervalo de max-age interno predeterminado de 7 días para las solicitudes que no se ha asignado una indicación de max-age en su Cache-Control o el encabezado Expires.
- Pagar toohello manera en la memoria caché de configuración se realiza un seguimiento, esta característica no se puede asociar con hello coincidencia condiciones siguientes: 
    - perimetral 
    - Cname
    - Literal de encabezado de solicitud
    - Carácter comodín de encabezado de solicitud
    - Método de solicitud
    - Literal de consulta de dirección URL
    - Carácter comodín de consulta de dirección URL

**Valor predeterminado:** 7 días

###<a name="expires-header-treatment"></a>Tratamiento del encabezado Expires
**Propósito:** controla la generación de Hola de encabezados Expires por un servidor perimetral cuando la característica de Max-Age externo está activa.

Hola tooachieve de manera más fácil este tipo de configuración es tooplace Hola Max-Age externo y características de tratamiento de encabezado expira hello en Hola la misma instrucción.

Valor|Resultado
--|--
Sobrescribir|Se garantiza que Hola siguientes acciones llevará a cabo:<br/>-Sobrescribe el encabezado Expires generado por el servidor de origen de Hola.<br/>: Agrega el encabezado Expires producido por la respuesta de hello externo Max-Age característica toohello.
Pass Through|Garantiza que el encabezado Expires producido por la característica de Max-Age externo Hola nunca es agregar toohello respuesta. <br/> Si el servidor de origen de hello genera un encabezado Expires, pasará a través de toohello por el usuario final. <br/>Si el servidor de origen de hello no genera un encabezado Expires, a continuación, esta opción puede contener un encabezado Expires toonot de encabezado de respuesta de hello causa.
Add if Missing| Si no se recibió un encabezado Expires desde el servidor de origen de hello, esta opción agrega el encabezado Expires producido por la característica de hello Max-Age externo. Esta opción es útil para garantizar que todos los recursos se asignarán a un encabezado Expires.
Remove| Garantiza que no se incluye con la respuesta de encabezado de hello un encabezado Expires. Si ya se ha asignado un encabezado Expires, se quitarán de la respuesta de encabezado de Hola.

**Comportamiento predeterminado**: sobrescribir.

###<a name="external-max-age"></a>Max-Age externa
**Propósito:** intervalo de max-age determina hello para la revalidación de la caché de explorador tooedge server. En otras palabras, puede comprobar la cantidad de Hola de tiempo que transcurrirá antes de un explorador para una nueva versión de un activo a partir de un servidor perimetral.

Si habilita esta característica generará caché-Control: max-age y expira encabezados desde nuestros servidores de borde y enviarlas cliente toohello HTTP. De forma predeterminada, estos encabezados sobrescribirán los creados por el servidor de origen de Hola. Sin embargo, el tratamiento de encabezado Cache-Control y las características de tratamiento de encabezado expira pueden ser tooalter usado este comportamiento.

Información importante:

- Esta acción no afecta a las nuevas validaciones de caché de servidor de tooorigin del servidor perimetral. Estos tipos de nuevas validaciones vienen determinados por los encabezados de Control de caché/Expires recibidos del servidor de origen de Hola y pueden personalizarse con el valor predeterminado interno Max-Age y las características de fuerza interna Max-Age.
- Configurar esta característica hace especificando un valor entero y seleccionando la unidad de tiempo deseado de hello (es decir, segundos, minutos, horas, etcetera).
- Este valor característica tooa negativo hace nuestro toosend de servidores de borde una memoria caché-Control: n-caché y una hora de Expires que se establece en hello pasado con cada explorador toohello de respuesta. Aunque un cliente HTTP no almacenará en memoria caché respuesta hello, esta configuración no tendrá ningún efecto capacidad toocache Hola respuesta nuestro servidor perimetral del servidor de origen Hola.
- Unidad de tiempo de configuración Hola demasiado "Off" deshabilitará esta característica. Los encabezados de caché-Control/Expires almacenado en caché con la respuesta de saludo del servidor de origen de hello pasará a través del explorador de toohello.

**Comportamiento predeterminado:** desactivado

###<a name="force-internal-max-age"></a>Forzar Max-Age interna
**Propósito:** intervalo de max-age determina hello para la revalidación de la caché de servidor de borde server tooorigin. Cantidad de tiempo que transcurrirá antes de que un servidor perimetral puede comprobar si un recurso almacenado en caché coincide con asset Hola almacenado en el servidor de origen de Hola se hello en otras palabras.

Información importante:

- Esta característica invalidará el intervalo de saludo max-age definido en encabezados Expires generados a partir de un servidor de origen o de Cache-Control.
- Esta característica no afecta a las nuevas validaciones de caché del servidor de tooedge de explorador. Estos tipos de nuevas validaciones vienen determinados por el encabezado Cache-Control o Expires encabezados enviaron toohello explorador.
- Esta característica no tiene un efecto notable en respuesta Hola entregado por un solicitante de toohello del servidor de borde. Sin embargo, puede tener un efecto en la cantidad de Hola de revalidación el tráfico enviado desde el servidor de origen de arista servidores toohello.
- Para configurar esta característica:
    - Seleccionar el código de estado de hello para el que se aplicará una max-age interno.
    - Especifica un valor entero y selecciona Hola unidad de tiempo que desee (por ejemplo, segundos, minutos, horas, etcetera). Este valor define el intervalo de la vigencia máxima de la solicitud de saludo.

- Unidad de tiempo de configuración Hola demasiado "Off" deshabilita esta característica. No se le asignará un intervalo de max-age interno toorequested activos. Si el encabezado original hello no incluye instrucciones de almacenamiento en caché, a continuación, asset Hola se almacenarán en caché según toohello configuración activa en la característica predeterminado interno Max-Age.
- Pagar toohello manera en la memoria caché de configuración se realiza un seguimiento, esta característica no se puede asociar con hello coincidencia condiciones siguientes: 
    - perimetral 
    - Cname
    - Literal de encabezado de solicitud
    - Carácter comodín de encabezado de solicitud
    - Método de solicitud
    - Literal de consulta de dirección URL
    - Carácter comodín de consulta de dirección URL

**Comportamiento predeterminado:** desactivado

###<a name="h264-support-http-progressive-download"></a>Compatibilidad de H.264 (Descarga progresiva de HTTP)
**Propósito:** determina los tipos de Hola de H.264 formatos de archivo que pueden ser usado toostream contenido.

Información importante:

- Defina un conjunto de extensiones de nombre de archivo H.264 permitidas, delimitadas por espacios, en la opción File Extensions (Extensiones de archivo). La opción de extensiones de archivo invalidará el comportamiento predeterminado de Hola. Para mantener la compatibilidad con MP4 y F4V, incluya esas extensiones de nombre de archivo al establecer esta opción. 
- Asegúrese de que tooinclude un punto al especificar cada extensión de nombre de archivo (por ejemplo,. mp4 F4V).

**Comportamiento predeterminado:** la descarga progresiva HTTP es compatible con medios MP4 y F4V de forma predeterminada.

###<a name="honor-no-cache-request"></a>Respetar solicitud de no almacenar en caché
**Propósito:** determina si las solicitudes de no almacenar en caché de un cliente HTTP se reenviarán toohello del servidor de origen.

Una solicitud de caché no se produce cuando el cliente de hello HTTP envía una memoria caché-Control: n-caché o pragma: encabezado de caché de solicitud de hello HTTP.

Valor|Resultado
--|--
habilitado|Permite no almacenar en caché de un cliente HTTP las solicitudes toobe toohello reenviado del servidor de origen y servidor de origen de hello devolverá los encabezados de respuesta de Hola y el cuerpo de Hola a través del servidor perimetral de Hola cliente toohello espera HTTP.
Disabled|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es tooprevent las solicitudes de caché no se reenvíen toohello del servidor de origen.

Para todo el tráfico de producción, es muy recomendable tooleave esta característica en su estado deshabilitado de forma predeterminada. En caso contrario, los servidores de origen no se pudo blindar de los usuarios finales que accidentalmente pueden desencadenar muchas solicitudes de caché no al actualizar las páginas web, o de hello muchos reproductores multimedia populares que están codificadas toosend un encabezado sin caché con cada solicitud de vídeo. No obstante, esta característica puede ser almacenamiento provisional no es de producción de toocertain tooapply útil o pruebas de directorios, en orden tooallow toobe de contenido nuevo extraen a petición del servidor de origen de Hola.

estado de la caché Hola que aparecerán para una solicitud que se permite el servidor de origen de tooan toobe reenviado debido toothis característica es TCP_Client_Refresh_Miss. El informe de Estados de memoria caché, que está disponible en el módulo de informe de núcleo de hello, proporciona información estadística por estado de la caché. Esto le permite número de hello tootrack y el porcentaje de solicitudes que se reenvían tooan del servidor de origen debido toothis característica.

**Comportamiento predeterminado**: deshabilitado.

###<a name="ignore-origin-no-cache"></a>Ignorar no almacenar en caché de origen
**Propósito:** determina si se pasan por alto la CDN Hola siguiendo directivas atendidas por un servidor de origen:

- Cache-Control: private
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

Información importante:

- Configurar esta característica mediante la definición de una lista delimitada por espacios de los códigos de estado para el que se pasará por alto Hola por encima de las directivas.
- Hello conjunto de códigos de estados válidos para esta característica son: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 y 505.
- Deshabilitar esta característica estableciendo el valor en blanco tooa.
- Pagar toohello manera en la memoria caché de configuración se realiza un seguimiento, esta característica no se puede asociar con hello coincidencia condiciones siguientes: 
    - perimetral 
    - Cname
    - Literal de encabezado de solicitud
    - Carácter comodín de encabezado de solicitud
    - Método de solicitud
    - Literal de consulta de dirección URL
    - Carácter comodín de consulta de dirección URL

**Comportamiento predeterminado:** el comportamiento predeterminado es hello toohonor por encima de las directivas.

###<a name="ignore-unsatisfiable-ranges"></a>Ignorar intervalos que no se puedan satisfacer 
**Propósito:** determina la respuesta de Hola que se devolverán tooclients cuando una solicitud genera un código de estado 416 intervalo no se puede satisfacer solicitado.

De forma predeterminada, este código de estado se devuelve cuando Hola especificado no puede satisfacer la solicitud de intervalo de bytes con un servidor perimetral y no se ha especificado un campo de encabezado de solicitud If-Range.

Valor|Resultado
-|-
habilitado|Evita que nuestros servidores de borde de solicitud de intervalo de bytes no válida de tooan responde con un código de estado 416 intervalo no se puede satisfacer solicitado. En su lugar nuestros servidores se entregar Hola solicitado activo y devolver un 200 OK al cliente de Hola.
Disabled|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es toohonor el código de estado 416 intervalo no se puede satisfacer solicitado.

**Comportamiento predeterminado**: deshabilitado.

###<a name="internal-max-stale"></a>Max-Stale interna
**Propósito:** controla cuánto tiempo pasado tiempo de expiración normal de hello un recurso almacenado en caché puede servirse desde un servidor perimetral al servidor perimetral de hello es hello de toorevalidate no se puede almacena en caché activo con el servidor de origen de Hola.

Normalmente, cuando se agota el tiempo de duración máxima de un recurso, servidor perimetral de hello enviará un servidor de origen revalidación toohello de solicitud. Hello del servidor de origen, a continuación, responderá con ya sea un 304 no modificado para asignar hello borde servidor una nueva concesión en activo en caché de hello, o bien con 200 OK para proporcionar una hello borde servidor con una versión actualizada del recurso almacenado en caché de Hola.

Si servidor perimetral de hello es no se puede tooestablish una conexión con el servidor de origen de hello al intentar una validación de este tipo, esta característica obsoleta de Max interno controla si y para hello cuánto, servidor perimetral puede continuar activo de tooserve Hola ahora obsoleta.

Tenga en cuenta que este intervalo de tiempo se inicia cuando expira la vigencia máxima del recurso de hello, no cuando hello revalidación error se produce. Por lo tanto, período máximo de Hola durante el cual puede proporcionarse un activo sin validación satisfactoria es cantidad Hola de tiempo especificado por la combinación de Hola de max-age más max obsoleta. Por ejemplo, si un recurso se almacenó en caché a las 9:00 con una antigüedad máxima de 30 minutos y una desusada máximo de 15 minutos, y luego intente una nueva validación errores en 9:44, se crearán un por el usuario final receptora Hola obsoletos almacenados en caché activo, mientras que produciría un intento de revalidación de los errores a las 9:46 Hola recibir un 504 tiempo de espera de puerta de enlace al usuario final.

Cualquier valor configurado para esta característica es sustituida por la memoria caché-Control: debe-volver a validar o almacenar en caché-Control: proxy-volver a validar encabezados recibidos desde el servidor de origen de Hola. Si cualquiera de los encabezados se recibe del servidor de origen de hello cuando inicialmente se almacena en caché de un recurso, servidor perimetral de hello no dará servicio un activo obsoleto almacenados en caché. En tal caso, si servidor perimetral de hello es no se puede toorevalidate con el origen de hello cuando ha transcurrido el intervalo de max-age del recurso de hello, a continuación, hello borde servidor devolverá un 504 tiempo de espera de puerta de enlace.

Información importante:

- Para configurar esta característica:
    - Seleccionar el código de estado de hello para el que se aplicará una max-desusada.
    - Especificar un valor entero y, a continuación, seleccionar Hola unidad de tiempo que desee (por ejemplo, segundos, minutos, horas, etcetera). Este valor define Hola interno máximo estables que se aplicará.

- Unidad de tiempo de configuración Hola demasiado "Off" deshabilitará esta característica. No se proporcionarán recursos almacenados en caché más allá de la fecha de expiración normal.
- Pagar toohello manera en la memoria caché de configuración se realiza un seguimiento, esta característica no se puede asociar con hello coincidencia condiciones siguientes: 
    - perimetral 
    - Cname
    - Literal de encabezado de solicitud
    - Carácter comodín de encabezado de solicitud
    - Método de solicitud
    - Literal de consulta de dirección URL
    - Carácter comodín de consulta de dirección URL

**Comportamiento predeterminado:** 2 minutos

###<a name="partial-cache-sharing"></a>Uso compartido de caché parcial
**Propósito**: determina si una solicitud puede generar contenido almacenado parcialmente en caché.

Esta caché parcial, a continuación, puede ser usado toofulfill nuevas solicitudes de contenido hasta Hola solicita contenido totalmente se almacena en caché.

Valor|Resultado
-|-
Enabled|Las solicitudes pueden generar contenido almacenado parcialmente en caché.
Disabled|Solamente pueden generar un totalmente en caché las solicitudes de versión de hello solicita contenido.

**Comportamiento predeterminado**: deshabilitado.

###<a name="prevalidate-cached-content"></a>PreValidate contenido en caché
**Propósito**: determina si el contenido almacenado en caché será apto para la revalidación temprana antes de que expire su período de vida.

Define la cantidad de Hola de tiempo de expiración toohello anteriores de hello solicitó TTL del contenido durante el cual será apto para la revalidación de los primeros.

Información importante:

- Al seleccionar "Off" como unidad de tiempo de hello requiere lugar de revalidación tootake después de que ha expirado el período de vida del contenido almacenado en memoria caché de Hola. No se debe especificar tiempo y se pasará por alto.

**Comportamiento predeterminado:** desactivado. Revalidación solo puede tener lugar después de hello ha expirado el período de vida del contenido almacenado en caché.

###<a name="refresh-zero-byte-cache-files"></a>Actualizar archivos de caché de cero bytes
**Propósito**: determina cómo nuestros servidores perimetrales controlan la solicitud de un cliente HTTP para un recurso de la caché de 0 bytes.

Los valores válidos son:

Valor|Resultado
--|--
habilitado|Hace que el recurso de hello borde toore fetch de servidor del servidor de origen de Hola.
Disabled|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es tooserve los activos de caché válida tras la solicitud.
Esta característica no es necesaria para la entrega de contenido y un almacenamiento en caché correcto, pero puede resultar útil para solucionar este problema. Por ejemplo, los generadores de contenido dinámicos en servidores de origen pueden producir accidentalmente en las respuestas de 0 bytes que se envían a servidores de borde de toohello. Normalmente, nuestros servidores perimetrales almacenan estos tipos de respuestas en caché. Si sabe que una respuesta de 0 bytes nunca es una respuesta válida 

a continuación, para este tipo de contenido, esta característica puede impedir que estos tipos de activos servirlo tooyour clientes.

**Comportamiento predeterminado**: deshabilitado.

###<a name="set-cacheable-status-codes"></a>Establecer códigos de estado almacenables en caché
**Propósito:** define Hola conjunto de códigos de estado que puede dar lugar a contenido almacenado en caché.

De forma predeterminada, el almacenamiento en caché solo está habilitado para las respuestas 200 OK.

Defina un conjunto de códigos de estado deseado de hello delimitada por espacios.

Información importante:

- Habilite también la característica Ignorar no almacenar en caché de origen. Si esa característica no está habilitada, las respuestas 200 OK podrían no almacenarse en caché.
- Hello conjunto de códigos de estados válidos para esta característica son: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 y 505.
- Esta característica no puede ser usado toodisable almacenamiento en caché para las respuestas que generan un código de estado OK 200.

**Comportamiento predeterminado:** el almacenamiento en caché solo está habilitado para las respuestas que generan un código de estado 200 OK.
###<a name="stale-content-delivery-on-error"></a>Entrega de contenido obsoleto en caso de error
**Propósito**: 

Determina si expirado contenido almacenado en caché se entregará cuando se produce un error durante la revalidación de caché o cuando Hola recuperar solicita contenido desde el servidor de origen del cliente de Hola.

Valor|Resultado
-|-
habilitado|Contenido obsoleto se servirá a toohello solicitante cuando se produce un error durante un servidor de origen de tooan de conexión.
Disabled|error del servidor de origen de Hola se reenviarán a toohello solicitante.

**Comportamiento predeterminado**: deshabilitado.

###<a name="stale-while-revalidate"></a>Obsoleto durante revalidación
**Propósito:** mejora el rendimiento al permitir que nuestros servidores perimetrales tooserve toohello contenido obsoleto solicitante mientras revalidación lleva a cabo.

Información importante:

- comportamiento de Hola de esta característica varía en unidad de tiempo seleccionado toohello correspondiente.
    - **Unidad de tiempo:** especificar un intervalo de tiempo y seleccione una hora unidad (por ejemplo, segundos, minutos, horas, etc.) tooallow obsoletos entrega de contenido. Este tipo de instalación permite Hola CDN tooextend Hola duración de tiempo que puede entregar contenido antes de requerir la validación según toohello siguiente fórmula:**TTL** + **tiempo volver a validar mientras obsoletos** 
    - **OFF:** seleccione "Off" revalidación toorequire antes de la solicitud de contenido obsoleto puede procesarse.
        - No especifique un período de tiempo ya que no es aplicable y se pasará por alto.

**Comportamiento predeterminado:** desactivado. Revalidación debe realizarse antes de Hola solicitado se puede atender contenido.

###<a name="comment"></a>Comentario
**Propósito:** permite un toobe tenga en cuenta que se agregan dentro de una regla.

Un uso de esta característica es tooprovide obtener información adicional sobre el uso general de Hola de una regla o por qué coincidir con una determinada condición o una característica se agregó la regla toohello.

Información importante:

- Se puede especificar un máximo de 150 caracteres.
- Asegúrese de que tooonly utilice caracteres alfanuméricos.
- Esta característica no afectan al comportamiento de Hola de regla de Hola. Se trata simplemente tooprovide un área donde puede proporcionar información para futuras referencias o que puede ayudar al solucionar problemas de regla de Hola.
 
## <a name="headers"></a>Encabezados

Estas características están diseñada tooadd, modificar o eliminar encabezados de solicitud de Hola o de respuesta.

Nombre | Propósito
-----|--------
Encabezado de respuesta Age | Determina si un encabezado de respuesta de edad se incluirán en la respuesta de hello enviado a toohello solicitante.
Depurar encabezados de respuesta de la caché | Determina si una respuesta puede incluir el encabezado de respuesta de X-CE-Debug de Hola que proporciona información sobre la directiva de caché de Hola para hello solicitado activo.
Modificar encabezado de solicitud de cliente | Sobrescribe, agrega o elimina un encabezado en una solicitud.
Modificar encabezado de respuesta de cliente | Sobrescribe, agrega o elimina un encabezado en una respuesta.
Establecer encabezado personalizado de IP de cliente | Permite dirección IP de hello del cliente solicitante hello toobe toohello agregado solicitud como un encabezado de solicitud personalizado.

###<a name="age-response-header"></a>Encabezado de respuesta Age
**Propósito**: determina si un encabezado de respuesta de edad se incluirán en hello respuesta enviada toohello solicitante.
Valor|Resultado
--|--
habilitado | encabezado de respuesta de edad de Hola se incluirán en la respuesta de hello enviado a toohello solicitante.
Disabled | encabezado de respuesta de edad de Hola se excluirá de respuesta de hello enviado a toohello solicitante.

**Comportamiento predeterminado**: deshabilitado.

###<a name="debug-cache-response-headers"></a>Depurar encabezados de respuesta de la caché
**Propósito:** determina si una respuesta puede incluir el encabezado de respuesta X-CE-Debug que proporciona información sobre la directiva de caché de Hola para hello solicitado activo.

Depurar encabezados se incluirán en la respuesta de hello cuando se cumplen los siguientes Hola la respuesta en caché:

- Hola depurar característica de encabezados de respuesta de caché se ha habilitado en la solicitud deseado Hola.
- Hola por encima de la solicitud define conjunto Hola de encabezados de respuesta de caché de depuración que se incluirán en la respuesta de Hola.

Depurar la respuesta en caché encabezados se pueden solicitar mediante la inclusión de hello después de encabezado y Hola deseadas directivas de solicitud de hello:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Ejemplo:**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Valor|Resultado
-|-
Enabled|Las solicitudes de encabezados de respuesta de caché de depuración devolverán una respuesta que incluye el encabezado X-EC-Debug.
Disabled|El encabezado de respuesta X-CE-Debug se excluirá de respuesta de Hola.

**Comportamiento predeterminado**: deshabilitado.

###<a name="modify-client-response-header"></a>Modificar encabezado de respuesta de cliente
**Propósito:** cada solicitud contiene un conjunto de [encabezados de solicitud]() que la describen. Esta característica puede:

- Anexar o sobrescribir el valor de hello asignado tooa encabezado de solicitud. Si no existe el encabezado de solicitud especificado hello, a continuación, esta característica lo agregará toohello solicitud.
- Eliminar un encabezado de solicitud de solicitud de saludo.

Las solicitudes que se reenvían tooan del servidor de origen reflejan los cambios de hello realizados por esta característica.

Una de las siguientes acciones de Hola puede realizarse en un encabezado de solicitud:

Opción|Descripción|Ejemplo
-|-|-
Append|Hola especificados se agregarán valor extremo del valor del encabezado de solicitud existente de Hola.|**Valor de encabezado de solicitud (cliente):**Valor1 <br/> **Valor de encabezado de solicitud (motor de reglas HTTP):**Valor2 <br/>**Nuevo valor de encabezado de solicitud:**Valor1Valor2
Sobrescribir|solicitud de Hola se utilizará el valor de encabezado toohello de conjunto de valor especificado.|**Valor de encabezado de solicitud (cliente):**Valor1 <br/>**Valor de encabezado de solicitud (motor de reglas HTTP):**Valor2 <br/>**Nuevo valor de encabezado de solicitud:**Valor2 <br/>
Eliminar|Elimina el encabezado de solicitud especificado Hola.|**Valor de encabezado de solicitud (cliente):**Valor1 <br/> **Modificar configuración de encabezado de solicitud de cliente:** encabezado de solicitud de eliminación hello en cuestión. <br/>**Resultado:** Hola especifica el encabezado de solicitud no se reenviarán toohello del servidor de origen.

Información importante:

- Asegúrese de que valor de Hola especificado en la opción de nombre es una coincidencia exacta para el encabezado de solicitud deseado de Hola.
- Caso no se tiene en cuenta para el propósito de Hola de identificación de un encabezado. Por ejemplo, cualquiera de hello siguiendo las variaciones del nombre de encabezado Cache-Control puede ser usado tooidentify:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Asegúrese de tooonly que utilice caracteres alfanuméricos, guiones o caracteres de subrayado para especificar un nombre de encabezado.
- Si elimina un encabezado impedirá que se va a reenviar el servidor de origen tooan por nuestros servidores de borde.
- Hello encabezados siguientes están reservados y no se puede modificar esta característica:
    - forwarded
    - host
    - via
    - Warning (Advertencia)
    - x-forwarded-for
    - Todos los nombres de encabezado que empiezan por "x-ce" están reservados.

###<a name="modify-client-response-header"></a>Modificar encabezado de respuesta de cliente
Cada respuesta contiene un conjunto de [encabezados de respuesta]() que lo describen. Esta característica puede:

- Anexar o sobrescribir el valor de hello asignado tooa encabezado de respuesta. Si no existe el encabezado de solicitud especificado hello, a continuación, esta característica lo agregará toohello respuesta.
- Eliminar un encabezado de respuesta de respuesta de Hola.

De forma predeterminada, los valores de encabezado de respuesta se definen por un servidor de origen y por nuestros servidores perimetrales.

Una de las siguientes acciones de Hola puede realizarse en un encabezado de respuesta:

Opción|Descripción|Ejemplo
-|-|-
Append|Hola especificados se agregarán valor extremo del valor del encabezado de solicitud existente de Hola.|**Valor de encabezado de respuesta (cliente):**Valor1 <br/> **Valor de encabezado de respuesta (motor de reglas HTTP):**Valor2 <br/>**Nuevo valor de encabezado de respuesta:**Valor1Valor2
Sobrescribir|solicitud de Hola se utilizará el valor de encabezado toohello de conjunto de valor especificado.|**Valor de encabezado de respuesta (cliente):**Valor1 <br/>**Valor de encabezado de respuesta (motor de reglas HTTP):**Valor2 <br/>**Nuevo valor de encabezado de respuesta:**Valor2 <br/>
Eliminar|Elimina el encabezado de solicitud especificado Hola.|**Valor de encabezado de solicitud (cliente):**Valor1 <br/> **Modificar configuración de encabezado de solicitud de cliente:** encabezado de respuesta de eliminación hello en cuestión. <br/>**Resultado:** Hola especificado no se reenviarán toohello solicitante al encabezado de respuesta.

Información importante:

- Asegúrese de que valor Hola especificado en la opción de nombre es una coincidencia exacta para el encabezado de respuesta deseada de Hola. 
- Caso no se tiene en cuenta para el propósito de Hola de identificación de un encabezado. Por ejemplo, cualquiera de hello siguiendo las variaciones del nombre de encabezado Cache-Control puede ser usado tooidentify:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Si elimina un encabezado impedirá que se va a reenviar toohello solicitante.
- Hello encabezados siguientes están reservados y no se puede modificar esta característica:
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - fecha
    - server
    - trailer
    - transfer-encoding
    - upgrade
    - vary
    - via
    - Warning (Advertencia)
    - Todos los nombres de encabezado que empiezan por "x-ce" están reservados.

###<a name="set-client-ip-custom-header"></a>Establecer encabezado personalizado de IP de cliente
**Propósito:** agrega un encabezado personalizado que identifica el cliente solicitante Hola por solicitud de toohello de dirección IP.

La opción de nombre de encabezado define nombre Hola Hola personalizado del encabezado de solicitud donde se almacenará la dirección IP del cliente de Hola.

Esta característica permite que un cliente toofind de servidor de origen a direcciones IP del cliente a través de un encabezado de solicitud personalizado. Si la solicitud de Hola se sirve desde la memoria caché, servidor de origen de hello no ser informado de la dirección IP del cliente de Hola. Por lo tanto, se recomienda usar esta característica con ADN o con recursos que no se almacenarán en caché.

Asegúrese de que ese nombre de encabezado especificado de hello no coincide con ninguno de hello siguientes:

- Nombres de encabezado de solicitud estándar. Encontrará una lista de nombres de encabezado estándar en [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Nombres de encabezado reservados:
    - forwarded-for
    - host
    - vary
    - via
    - Warning (Advertencia)
    - x-forwarded-for
    - Todos los nombres de encabezado que empiezan por "x-ce" están reservados.
 
## <a name="logs"></a>Registros

Estas características son datos de hello toocustomize diseñada almacenados en archivos de registro sin procesar.

Nombre | Propósito
-----|--------
Campo de registro personalizado 1 | Determina el formato de Hola y el contenido de Hola que se va a asignar toohello campo de registro personalizado en un archivo de registro sin procesar.
Cadena de consulta del registro | Determina si una cadena de consulta se almacenará junto con la dirección URL de hello en los registros de acceso.

###<a name="custom-log-field-1"></a>Campo de registro personalizado 1
**Propósito:** determina el formato de Hola y el contenido de Hola que se va a asignar toohello campo de registro personalizado en un archivo de registro sin procesar.

propósito principal de Hello detrás de este campo personalizado es tooallow toodetermine qué valores de encabezado de solicitud y respuesta se almacenará en los archivos de registro.

De forma predeterminada, el campo de registro personalizado de Hola se denomina "x-ec_custom-1." Sin embargo, se puede personalizar nombre Hola de este campo desde el [página Configuración de registro sin procesar]().

Hola de formato que se deben usar los encabezados de solicitud y respuesta de toospecify se define a continuación.

Tipo de encabezado|Formato|Ejemplos
-|-|-
Encabezado de solicitud|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
Encabezado de respuesta|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

Información importante:

- Un campo de registro personalizado puede contener cualquier combinación de campos de encabezado y texto sin formato.
- Los caracteres válidos para este campo son siguiente hello: alfanumérico (es decir, 0-9, a-z y A-z), guiones, caracteres de dos puntos, punto y coma, apóstrofos, comas, puntos, caracteres de subrayado, signos igual, paréntesis, corchetes y espacios. Hello símbolo de porcentaje y llaves solo se permiten cuando usa toospecify un campo de encabezado.
- ortografía Hola para cada campo de encabezado especificado debe coincidir con nombre de encabezado de solicitud/respuesta deseada de Hola.
- Si desea que toospecify varios encabezados, a continuación, se recomienda que utilizar un separador tooindicate cada encabezado. Por ejemplo, podría utilizar una abreviatura para cada encabezado. Esta es una sintaxis de ejemplo.
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**Valor predeterminado** -:

###<a name="log-query-string"></a>Cadena de consulta del registro
**Propósito:** determina si una cadena de consulta se almacenará junto con la dirección URL de hello en los registros de acceso.

Valor|Resultado
-|-
habilitado|Permite el almacenamiento de Hola de cadenas de consulta cuando se graba las direcciones URL en un registro de acceso. Si una dirección URL no contiene una cadena de consulta, esta opción no tendrá efecto.
Disabled|Restaura el comportamiento predeterminado de Hola. comportamiento predeterminado de Hello es tooignore las cadenas de consulta cuando se graba las direcciones URL en un registro de acceso.

**Comportamiento predeterminado**: deshabilitado.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origen

Estas características están diseñada toocontrol cómo CDN Hola se comunica con un servidor de origen.

Nombre | Propósito
-----|--------
Número máximo de solicitudes de conexión persistente | Define el número máximo de Hola de solicitudes para una conexión Keep-Alive antes de cerrarlo.
Encabezados de proxy especiales | Define el conjunto de hello específica de la red CDN de encabezados de solicitud que se reenvían desde un servidor de origen de tooan de servidor perimetral.


###<a name="maximum-keep-alive-requests"></a>Número máximo de solicitudes de conexión persistente
**Propósito:** define el número máximo de Hola de solicitudes para una conexión Keep-Alive antes de cerrarlo.

Establecer número máximo de Hola de valor bajo de solicitudes tooa no es recomendable y puede provocar una degradación del rendimiento.

Información importante:

- Especifique este valor como un número entero.
- Hola especificado no incluir comas o períodos de valor.

**Valor predeterminado:** 10.000 solicitudes

###<a name="proxy-special-headers"></a>Encabezados de proxy especiales
**Propósito:** define el conjunto de Hola de [encabezados de solicitud específica de la red CDN]() que se reenvían desde un servidor de origen de tooan de servidor perimetral.

Información importante:

- Cada encabezado de solicitud específico de la red CDN definido en esta característica se reenviarán tooan del servidor de origen.
- Impedir que un encabezado de solicitud específico de la red CDN se reenvíe tooan del servidor de origen mediante la eliminación de esta lista.

**Comportamiento predeterminado:** todos los [encabezados de solicitud específica de la red CDN]() se reenviarán toohello del servidor de origen.

## <a name="specialty"></a>Especialidad

Estas características ofrecen funcionalidad avanzada que solo deben utilizar los usuarios avanzados.

Nombre | Propósito
-----|--------
Métodos HTTP almacenables en caché | Determina el conjunto de Hola de métodos HTTP adicionales que pueden almacenarse en caché en nuestra red.
Tamaño del cuerpo de solicitud almacenable en caché | Define el umbral de Hola para determinar si se puede almacenar en caché una respuesta POST.

###<a name="cacheable-http-methods"></a>Métodos HTTP almacenables en caché
**Propósito:** determina Hola conjunto de métodos HTTP adicionales que pueden almacenarse en caché en nuestra red.

Información importante:

- Esta característica da por supuesto que las respuestas GET siempre deben almacenarse en caché. Como resultado, Hola método HTTP GET no se debe incluir al establecer esta característica.
- Esta característica solo admite el método HTTP POST de Hola. Para habilitar el almacenamiento en caché de la respuesta POST, establezca esta característica en POST. 
- De forma predeterminada, solo se almacenarán en caché las solicitudes cuyo cuerpo sea inferior a 14 Kb. Use la característica de tamaño de cuerpo de solicitud almacenable en caché para establecer el tamaño del cuerpo de solicitud máximo Hola.

**Comportamiento predeterminado:** solo se almacenarán en caché las respuestas GET.

###<a name="cacheable-request-body-size"></a>Tamaño del cuerpo de solicitud almacenable en caché

**Propósito:** define umbral de Hola para determinar si se puede almacenar en caché una respuesta POST.

Este umbral se determina especificando un tamaño máximo de cuerpo de solicitud. Las solicitudes que contengan un cuerpo de solicitud más grandes no se almacenarán en caché.

Información importante:

- Esta característica solo es aplicable cuando las respuestas POST son aptas para su almacenamiento en caché. Use Hola característica de métodos HTTP almacenable en caché para habilitar el almacenamiento en caché de la solicitud POST.
- cuerpo de la solicitud de saludo se tiene en cuenta para:
    - valores x-www-form-urlencoded
    - Garantizar una clave de caché única
- Definir un tamaño de cuerpo de solicitud máximo grande puede afectar al rendimiento de la entrega de datos.
    - **Valor recomendado:** 14 Kb
    - **Valor mínimo:** 1 Kb

**Comportamiento predeterminado:** 14 Kb
 
## <a name="url"></a>URL

Estas características permiten un toobe solicitud redirigida o volver a escribir tooa otra dirección URL.

Nombre | Propósito
-----|--------
Seguir redireccionamientos | Determina si las solicitudes pueden ser el nombre de host de toohello redirigido definido en el encabezado de ubicación de hello devuelto por un servidor de origen del cliente.
Redirección de URL | Redirige las solicitudes a través del encabezado de ubicación de Hola.
Reescritura de direcciones URL  | Reescribe la dirección URL de solicitud de saludo.

###<a name="follow-redirects"></a>Seguir redireccionamientos
**Propósito:** determina si las solicitudes pueden ser el nombre de host de toohello redirigida definida en el encabezado de ubicación devuelto por un servidor de origen del cliente.

Información importante:

- Las solicitudes solo pueden ser redirigido tooedge CNAME que corresponden toohello misma plataforma.

Valor|Resultado
-|-
Enabled|Las solicitudes se pueden redirigir.
Disabled|Las solicitudes no se redirigirán.

**Comportamiento predeterminado**: deshabilitado.
###<a name="url-redirect"></a>Redirección de URL
**Propósito**: redirige las solicitudes a través del encabezado Ubicación.

configuración de Hola de esta característica requiere establecer las siguientes opciones de hello:

Opción|Descripción
-|-
Código|Seleccione el código de respuesta de Hola que se devolverán a toohello solicitante.
Origen y patrón| Esta configuración define un patrón URI de solicitud que identifica el tipo de Hola de solicitudes que se pueden redirigir. Solo las solicitudes cuya dirección URL satisface ambas Hola siguiendo criterios se redirigirán: <br/> <br/> **Origen:** (o punto de acceso al contenido) seleccione una ruta de acceso relativa que identifique un servidor de origen. Se trata de sección de "/XXXX/" hello y su nombre de punto de conexión. <br/> **Origen (patrón):** se debe definir un patrón que identifique las solicitudes por ruta de acceso relativa. Este patrón de expresión regular debe definir una ruta de acceso que se inicia directamente después de hello seleccionado previamente el punto de acceso al contenido (véase más arriba). <br/> -Asegúrese de que los criterios URI de solicitud de hello (es decir, origen y patrón) definen anteriormente no entra en conflicto con las condiciones de coincidencia definidas para esta característica. <br/> -Lograr toospecify seguro de que un modelo. Usar un valor en blanco como patrón de hello solamente se corresponderá con carpeta de raíz de toohello de solicitudes del servidor de origen seleccionado hello (p. ej., http://cdn.mydomain.com/).
Destino| Definir la dirección URL de Hola Hola toowhich por encima de las solicitudes se redirigirán. <br/> Construya esta dirección URL dinámicamente mediante: <br/> - Un patrón de expresión regular <br/>- Variables HTTP <br/> Sustituya los valores de hello capturados en el modelo de origen de hello en el patrón de destino de hello mediante $ _n_  donde  _n_  identifica un valor según el orden de hello en el que se capturaron. Por ejemplo, $1 representa el primer valor de hello capturado en el modelo de origen de hello, mientras $2 representa el segundo valor de Hola. <br/> 
Es muy recomendable toouse una dirección URL absoluta. uso de Hola de una dirección URL relativa puede redirigir la ruta de acceso de direcciones URL de CDN tooan no válido.

**Escenario de ejemplo**

En este ejemplo, demostraremos cómo tooredirect un borde de dirección URL de CNAME que resuelve toothis basar la dirección URL de la red CDN: http://marketing.azureedge.net/brochures

Calificar las solicitudes será redirigido toothis borde base URL CNAME: http://cdn.mydomain.com/resources

Esta redirección de dirección URL se puede lograr a través de hello siguiente configuración:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Puntos clave:**

- característica de redireccionamiento de direcciones URL de Hello define Hola direcciones URL que se redirigirán de solicitudes. Como resultado, no se necesitan otras condiciones de coincidencia. Aunque la condición de coincidencia de Hola se ha definido como "Siempre", solo solicita que toohello punto se redirigirá la carpeta de origen de cliente "marketing" hello "folletos". 
- Todas las solicitudes de búsqueda de coincidencias será borde toohello redirigida que CNAME URL definida en la opción de destino. 
    - Escenario de ejemplo 1: 
        - Solicitud de ejemplo (dirección URL de CDN): http://marketing.azureedge.net/brochures/widgets.pdf 
        - URL de solicitud (después de la redirección): http://cdn.mydomain.com/resources/widgets.pdf  
    - Escenario de ejemplo 2: 
        - Solicitud de ejemplo (URL de servidor perimetral CNAME): http://marketing.mydomain.com/brochures/widgets.pdf 
        - URL de solicitud (después de la redirección): http://cdn.mydomain.com/resources/widgets.pdf Escenario de ejemplo
    - Escenario de ejemplo 3: 
        - Solicitud de ejemplo (URL de servidor perimetral CNAME): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - URL de solicitud (después de la redirección): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- variable del esquema de solicitud (% {esquema}) de Hola se aprovecha de la opción de destino. Esto garantiza que el esquema de la solicitud de ese hello no cambie después de la redirección.
- segmentos de dirección URL de Hola que se capturaron de solicitud de hello están anexados toohello nueva dirección URL a través de "$1".
 
###<a name="url-rewrite"></a>Reescritura de direcciones URL
**Propósito:** reescribe la dirección URL de solicitud de saludo.

Información importante:

- configuración de Hola de esta característica requiere establecer las siguientes opciones de hello:

Opción|Descripción
-|-
 Origen y patrón | Esta configuración define un patrón URI de solicitud que identifica el tipo de Hola de solicitudes que se puede volver a escribir. Se reescribirán solo las solicitudes cuya dirección URL satisface ambas Hola siguiendo criterios: <br/>     - **Origen (o punto de acceso al contenido)**: seleccione una ruta de acceso relativa que identifique un servidor de origen. Se trata de sección de "/XXXX/" hello y su nombre de punto de conexión. <br/> - **Origen (patrón):** se debe definir un patrón que identifique las solicitudes por ruta de acceso relativa. Este patrón de expresión regular debe definir una ruta de acceso que se inicia directamente después de hello seleccionado previamente el punto de acceso al contenido (véase más arriba). <br/> Asegúrese de que no entren en conflicto Hola solicitud URI criterios (es decir, origen y patrón) definidos anteriormente con cualquiera de las condiciones de coincidencia de hello definidas para esta característica. Lograr toospecify seguro de que un modelo. Usar un valor en blanco como patrón de hello solamente se corresponderá con carpeta de raíz de toohello de solicitudes del servidor de origen seleccionado hello (p. ej., http://cdn.mydomain.com/). 
 Destino  |Definir la dirección URL relativa de Hola Hola toowhich por encima de las solicitudes se reescribirán por: <br/>    1. Seleccione un punto de acceso al contenido que identifique un servidor de origen. <br/>    2. Defina el uso de una ruta de acceso relativa: <br/>        - Un patrón de expresión regular <br/>        - Variables HTTP <br/> <br/> Sustituya los valores de hello capturados en el modelo de origen de hello en el patrón de destino de hello mediante $ _n_  donde  _n_  identifica un valor según el orden de hello en el que se capturaron. Por ejemplo, $1 representa el primer valor de hello capturado en el modelo de origen de hello, mientras $2 representa el segundo valor de Hola. 
 Esta característica permite a nuestros servidores perimetrales toorewrite Hola URL sin realizar una redirección tradicional. Esto significa que solicitante Hola recibirá Hola respuesta el mismo código como si hubiera ha solicitado la dirección URL de hello volver a escribir.

**Escenario de ejemplo 1**

En este ejemplo, demostraremos cómo tooredirect un borde de dirección URL de CNAME que resuelve toothis basar la dirección URL de la red CDN: http://marketing.azureedge.net/brochures/

Calificar las solicitudes será redirigido toothis borde base URL CNAME: http://MyOrigin.azureedge.net/resources/

Esta redirección de dirección URL se puede lograr a través de hello siguiente configuración:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Escenario de ejemplo 2**

En este ejemplo, demostraremos cómo tooredirect un borde de la dirección URL de CNAME de mayúsculas toolowercase mediante expresiones regulares.

Esta redirección de dirección URL se puede lograr a través de hello siguiente configuración:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Puntos clave:**

- característica de reescritura de direcciones URL de Hello define Hola solicitar direcciones URL que se escribirá. Como resultado, no se necesitan otras condiciones de coincidencia. Aunque la condición de coincidencia de Hola se ha definido como "Siempre", solo solicita que toohello punto se reescribirán carpeta de origen de cliente "marketing" hello "folletos".

- segmentos de dirección URL de Hola que se capturaron de solicitud de hello están anexados toohello nueva dirección URL a través de "$1".



###<a name="compatibility"></a>Compatibilidad

Esta característica incluye que coinciden con los criterios que deben cumplirse antes de solicitud tooa aplicada. En orden tooprevent al configurar los criterios de coincidencia en conflicto, esta característica es incompatible con hello coincidencia condiciones siguientes:

- Número de sistema autónomo (AS)
- Origen de red CDN
- Dirección IP de cliente
- Origen de cliente
- Esquema de solicitud
- Directorio de ruta de acceso URL
- Extensión de ruta de acceso URL
- Nombre de archivo de ruta de acceso URL
- Literal de ruta de acceso URL
- Regex de ruta de acceso URL
- Carácter comodín de ruta de acceso URL
- Literal de consulta de dirección URL
- Parámetro de consulta de dirección URL
- Regex de consulta de dirección URL
- Carácter comodín de consulta de dirección URL


## <a name="next-steps"></a>Pasos siguientes
* [Referencia del motor de reglas](cdn-rules-engine-reference.md)
* [Expresiones condicionales del motor de reglas](cdn-rules-engine-reference-conditional-expressions.md)
* [Condiciones de coincidencia del motor de reglas](cdn-rules-engine-reference-match-conditions.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
* [Información general de la red CDN de Azure](cdn-overview.md)
