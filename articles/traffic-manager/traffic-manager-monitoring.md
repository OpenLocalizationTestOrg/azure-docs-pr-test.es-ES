---
title: "supervisión de extremos de Traffic Manager aaaAzure | Documentos de Microsoft"
description: "En este artículo puede ayudarle a entender cómo Traffic Manager utiliza supervisión de extremos y toohelp de conmutación por error de punto de conexión automática Azure los clientes implementar aplicaciones de alta disponibilidad"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Supervisión de puntos de conexión de Traffic Manager

El Administrador de tráfico de Azure incluye la supervisión de puntos de conexión integrados y la conmutación por error automática de los puntos de conexión. Esta característica ayuda a proporcionar aplicaciones de alta disponibilidad que un error tooendpoint resistente, incluidos los errores de la región de Azure.

## <a name="configure-endpoint-monitoring"></a>Configuración de la supervisión de los puntos de conexión

supervisión de extremos de tooconfigure, debe especificar Hola después de configuración en el perfil de Traffic Manager:

* **Protocolo**. Elija HTTP, HTTPS o TCP como protocolo de Hola que utiliza el Administrador de tráfico al sondeo su punto de conexión toocheck su estado. La supervisión HTTPS no comprueba si el certificado SSL es válido, solo comprueba que Hola certificado está presente.
* **Port**. Elegir puerto de hello usado para la solicitud de saludo.
* **Ruta de acceso**. Esta opción de configuración solo es válida para hello protocolos HTTP y HTTPS, para los que es necesario especificar configuración de ruta de acceso de Hola. Proporciona esta opción para saludo TCP supervisión protocolo produce un error. Para el protocolo TCP, proporcione ruta de acceso relativa de Hola y nombre de Hola de página Web de Hola o archivo hello ese Hola accesos de supervisión. Una barra diagonal (/) es una entrada válida para la ruta de acceso relativa de Hola. Este valor implica que el archivo hello esté en el directorio raíz de hello (valor predeterminado).
* **Intervalo de sondeo**. Este valor especifica la frecuencia con la que el agente de sondeo de Traffic Manager comprueba el estado de un punto de conexión. Puede especificar dos valores aquí: 30 segundos (sondeo normal) y 10 segundos (sondeo rápido). Si no se proporciona ningún valor, el perfil de hello establece tooa valor de predeterminado de 30 segundos. Visite hello [Traffic Manager precios](https://azure.microsoft.com/pricing/details/traffic-manager) página toolearn más sobre los precios de búsqueda rápida.
* **Número tolerado de errores**. Este valor especifica cuántos errores tolera un agente de sondeo de Traffic Manager antes de marcar un punto de conexión como en mal estado. Su valor puede oscilar entre 0 y 9. Un valor de 0 significa que un único error de supervisión puede provocar que toobe extremo marcado como incorrecto. Si no se especifica ningún valor, usa el valor predeterminado de Hola de 3.
* **Tiempo de espera de supervisión**. Esta propiedad especifica la cantidad de Hola de hello Traffic Manager agente sondeo debe esperar antes de considerar que compruebe un error cuando un sondeo de comprobación de estado se envía el punto de conexión de toohello de tiempo. Si Hola que intervalo de sondeo se establece too30 segundos; a continuación, puede establecer el valor de tiempo de espera de hello entre 5 y 10 segundos. Si no se especifica ningún valor, el valor predeterminado será de 10 segundos. Si Hola que intervalo de sondeo se establece too10 segundos; a continuación, puede establecer el valor de tiempo de espera de hello entre 5 y 9 segundos. Si no se especifica ningún valor, el valor predeterminado será de 9 segundos.

![Supervisión de puntos de conexión de Traffic Manager](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Figura 1: supervisión de puntos de conexión de Traffic Manager**

## <a name="how-endpoint-monitoring-works"></a>Funcionamiento de la supervisión de puntos de conexión

Si Hola protocolo de supervisión se establece como HTTP o HTTPS, agente de sondeo de Traffic Manager de hello realiza un extremo de toohello de solicitud GET mediante Hola protocolo, puerto y ruta de acceso relativa indicada. Si recibe una respuesta 200-OK, ese punto de conexión se considera correcto. Si la respuesta de hello es un valor diferente, o, si se recibe ninguna respuesta dentro del período de tiempo de espera de hello especificado, a continuación, hello Traffic Manager probing agente vuelve a intentar según la configuración de tolerado número de errores de toohello (no vuelve a intentar terminado si este valor es 0) . Si Hola de errores consecutivos sea mayor que la configuración de tolerado número de errores de hello, ese punto de conexión está marcado como incorrecto. 

Si hello supervisión protocolo es TCP, agente de sondeo de Traffic Manager de hello inicia una solicitud de conexión TCP con el puerto de hello especificado. Si el punto de conexión de hello responde toohello solicitud con una conexión respuesta tooestablish hello, que comprobación de estado está marcada como una ejecución satisfactoria y agente de sondeo de Traffic Manager de hello restablece la conexión de TCP de Hola. Si la respuesta de hello es un valor diferente, o si se recibe ninguna respuesta dentro de período de tiempo de espera de hello especificado, Hola Traffic Manager probing agente vuelve a intentar según la configuración de tolerado número de errores de toohello (no vuelve a intentar se realiza si este valor es 0). Si Hola de errores consecutivos sea mayor que la configuración de hello tolerado número de errores, a continuación, ese punto de conexión se muestra como incorrecto.

En todos los casos, los sondeos de Traffic Manager desde varias ubicaciones y determinación de fallo consecutivo de hello ocurre dentro de cada región. Esto también significa que los puntos de conexión están recibiendo sondeos de estado desde el Administrador de tráfico con una frecuencia mayor que la configuración de hello usada para el intervalo de sondeo.

>[!NOTE]
>Para HTTP o HTTPS protocolo de supervisión, una práctica común en lado de punto de conexión de hello es tooimplement una página personalizada dentro de su aplicación, por ejemplo, /health.aspx. Con esta ruta de acceso para la supervisión, puede realizar comprobaciones específicas de la aplicación, como la comprobación de los contadores de rendimiento o la comprobación de disponibilidad de la base de datos. En función de estas comprobaciones personalizadas, página de hello devuelve un código de estado HTTP adecuado.

Todos los puntos de conexión de un perfil de Traffic Manager comparten la configuración de supervisión. Si necesita toouse diferentes de configuración de supervisión de extremos diferentes, puede crear [anidados perfiles de Traffic Manager](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Estado de los puntos de conexión y de los perfiles

Puede habilitar y deshabilitar los perfiles y los puntos de conexión del Administrador de tráfico. Sin embargo, como resultado de la configuración y los procesos automatizados del Administrador de tráfico, también podría producirse un cambio en el estado del punto de conexión.

### <a name="endpoint-status"></a>Estado del extremo

Puede habilitar o deshabilitar un punto de conexión específico. servicio subyacente Hello, que puede hallarse aún funciona correctamente, se ve afectada. Controles de estado de punto de conexión de variación Hola Hola disponibilidad de punto de conexión de Hola Hola perfil de Traffic Manager. Cuando se deshabilita un estado de punto de conexión, Traffic Manager no comprueba su estado y Hola extremo no estuviera incluido en una respuesta DNS.

### <a name="profile-status"></a>Estado del perfil

Con configuración de estado del perfil de hello, puede habilitar o deshabilitar un perfil específico. Mientras que el estado de punto de conexión afecta a un extremo único, el estado del perfil afecta a todo perfil hello, incluidos todos los extremos. Cuando se deshabilita un perfil, no se comprueban los puntos de conexión de hello para el estado y ningún punto de conexión se incluye en una respuesta DNS. Un [NXDOMAIN](https://tools.ietf.org/html/rfc2308) se devuelve el código de respuesta de consulta DNS de Hola.

### <a name="endpoint-monitor-status"></a>Estado de supervisión de punto de conexión

Supervisar el estado de punto de conexión es un valor generado por el Administrador de tráfico que muestra el estado de saludo del extremo de Hola. No se puede cambiar esta configuración manualmente. supervisar el estado de punto de conexión Hello es una combinación de resultados de Hola de supervisión de extremos y Hola estado de punto de conexión configurados. valores posibles de Hola de supervisar el estado de punto de conexión se muestran en hello en la tabla siguiente:

| Estado del perfil | Estado del extremo | Estado de supervisión de punto de conexión | Notas |
| --- | --- | --- | --- |
| Disabled |Enabled |Inactivo |se ha deshabilitado el perfil de Hola. Aunque el estado del extremo de hello está habilitado, el estado del perfil hello (deshabilitado) tiene prioridad. Los puntos de conexión en los perfiles Disabled no se supervisan. Se devuelve un código de respuesta NXDOMAIN para consulta DNS de Hola. |
| &lt;cualquiera&gt; |Disabled |Disabled |se ha deshabilitado el punto de conexión de Hola. Los puntos de conexión dehabilitados no se supervisan. Hola extremo no estuviera incluido en las respuestas DNS, por lo tanto, no recibe tráfico. |
| habilitado |Enabled |En línea |extremo de Hola se supervisa y está en buen estado. Se incluye en las respuestas DNS y, por tanto, puede recibir tráfico. |
| Enabled |Enabled |Degradado |Error en las comprobaciones de estado de supervisión de punto de conexión. punto de conexión de Hello no se incluye en las respuestas DNS y no recibe tráfico. <br>Un toothis de excepción es si se degradan todos los extremos, en cuyo caso todos ellos se consideran toobe devuelve en respuesta a la consulta hello).</br>|
| habilitado |Enabled |CheckingEndpoint |Hola extremo se supervisa, pero aún no han recibido resultados Hola del primer sondeo de Hola. CheckingEndpoint es un estado temporal que normalmente se produce inmediatamente después de agregar o habilitar un punto de conexión en el perfil de Hola. Un punto de conexión en este estado se incluye en las respuestas DNS y puede recibir tráfico. |
| Enabled |Enabled |Stopped |Hola nube servicio o aplicación web que Hola toois de puntos de extremo no se está ejecutando. Compruebe la configuración de aplicación web o servicio en la nube de Hola. Esto también puede ocurrir si el extremo hello es de tipo anidado de punto de conexión y perfil de hello secundario está deshabilitado o está inactivo. <br>Un punto de conexión en estado Detenido no se supervisa. No se incluye en las respuestas DNS y, por tanto, no recibe tráfico. Un toothis de excepción es si se degradan todos los extremos, en cuyo caso todas ellas se considerarán toobe devuelve en respuesta a la consulta Hola.</br>|

Para obtener más información sobre cómo se calcula el valor de estado de supervisión del punto de conexión en el caso de puntos de conexión anidados, consulte [Perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Estado de supervisión de perfiles

estado del monitor de perfil de Hello es una combinación del estado del perfil Hola configurado y valores de estado de monitor de punto de conexión de Hola para todos los extremos. en hello en la tabla siguiente se describen los valores posibles de Hello:

| Estado del perfil (según la configuración) | Estado de supervisión de punto de conexión | Estado de supervisión de perfiles | Notas |
| --- | --- | --- | --- |
| Disabled |&lt;cualquiera&gt; o un perfil sin puntos de conexión definidos. |Disabled |se ha deshabilitado el perfil de Hola. |
| habilitado |estado de Hola de al menos un extremo está degradado. |Degradado |Revise los valores de estado de hello extremo individual toodetermine qué extremos requiriesen atención adicional. |
| habilitado |estado de Hola de al menos un extremo está en línea. Ningún punto de conexión tiene un estado Degradado. |En línea |servicio de Hello está aceptando tráfico. No se requiere ninguna acción adicional. |
| habilitado |estado de Hola de al menos un extremo es CheckingEndpoint. Ningún punto de conexión está en estado En línea o Degradado. |CheckingEndpoints |Este estado de transición se produce cuando se crea o habilita un perfil. estado del extremo Hola se comprueba Hola primera vez. |
| habilitado |Estados de Hola de todos los extremos de perfil de hello están deshabilitados o detenidos o perfil de hello tiene ningún extremo definido. |Inactivo |Ningún punto de conexión está activa, pero Hola perfil todavía está habilitado. |

## <a name="endpoint-failover-and-recovery"></a>Conmutación por error y recuperación de un punto de conexión

Traffic Manager comprueba periódicamente mantenimiento Hola de cada punto de conexión, incluidos los puntos de conexión incorrecto. Traffic Manager detecta cuándo es correcto un punto de conexión y lo pone de nuevo en rotación.

Un punto de conexión está en mal estado cuando se produce alguno de hello siguientes eventos:
- Si Hola supervisión protocolo es HTTP o HTTPS:
    - Se recibe una respuesta distinta de 200 (incluidos un código 2xx diferente o un redireccionamiento 301/302).
- Si el protocolo de supervisión de hello es TCP: 
    - Una respuesta de confirmación o SYN ACK se recibe en la solicitud de sincronización de toohello de respuesta enviados por Traffic Manager tooattempt establecer una conexión.
- Tiempo de espera. 
- Cualquier otro problema de conexión resultante en el punto de conexión de hello no esté accesible.

Para más información sobre la solución de problemas de comprobaciones erróneas, consulte [Solución de problemas de estado degradado en el Administrador de tráfico de Azure](traffic-manager-troubleshooting-degraded.md). 

Hola siguiente escala de tiempo en la figura 2 es una descripción detallada del proceso de punto de conexión de administrador de tráfico cuya Hola después de la configuración de supervisión de hello: protocolo de supervisión es HTTP, intervalo de sondeo es de 30 segundos, el número de errores permitidos es 3, el valor de tiempo de espera es de 10 segundos y TTL de DNS es de 30 segundos.

![Secuencia de conmutación por error y conmutación por error de puntos de conexión del Administrador de tráfico](./media/traffic-manager-monitoring/timeline.png)

**Figura 2: secuencia de conmutación por error y recuperación de un punto de conexión con Traffic Manager**

1. **GET**. Para cada extremo, Hola sistema de supervisión de Traffic Manager realiza una solicitud GET en ruta de acceso de hello especificada en la configuración de supervisión de Hola.
2. **200 - CORRECTO**. sistema de supervisión de Hello espera un toobe de mensaje HTTP 200 OK devuelve dentro de 10 segundos. Cuando recibe esta respuesta, reconoce que el servicio de hello está disponible.
3. **30 segundos entre comprobaciones**. comprobación de estado de punto de conexión de Hola se repite cada 30 segundos.
4. **Servicio no disponible**. servicio de Hello deja de estar disponible. Traffic Manager no lo sabrá hasta la próxima comprobación de mantenimiento de Hola.
5. **Hola de tooaccess intentos supervisión de la ruta de acceso**. sistema de supervisión de Hello realiza una solicitud GET, pero no recibe una respuesta en el período de tiempo de espera de Hola de 10 segundos (o bien, puede ser recibe una respuesta distinta de 200). Después lo intenta tres veces en intervalos de 30 segundos. Si uno de los intentos de hello es correcta, se restablece el número de Hola de intentos.
6. **Estado establecido tooDegraded**. Después de un cuarto error consecutivo, sistema de supervisión de Hola marca estado de punto de conexión disponible de hello como degradado.
7. **El tráfico es tooother desviadas extremos**. Hello servidores de nombres DNS de Traffic Manager se actualizan y Traffic Manager ya no devuelve el punto de conexión de hello en las consultas de tooDNS de respuesta. Las nuevas conexiones están tooother dirigida, los puntos de conexión disponibles. En cambio, es posible que las respuestas DNS anteriores que incluyen este punto de conexión aún se puedan almacenar en caché por parte de servidores y clientes DNS recursivos. Los clientes siguen el punto de conexión de toouse Hola hasta que expire Hola memoria caché de DNS. Como expire Hola memoria caché de DNS, los clientes realizan nuevas consultas DNS y están toodifferent dirigido. duración de la caché de Hola se controla mediante la opción de TTL Hola Hola perfil de Traffic Manager, por ejemplo, 30 segundos.
8. **Continúan las comprobaciones de estado**. Traffic Manager seguirá toocheck mantenimiento de Hola de punto de conexión de hello aunque tiene un estado degradado. Traffic Manager detecta cuando el punto de conexión de hello devuelve toohealth.
9. **El servicio vuelve a estar en línea**. Hola servicio deja de estar disponible. punto de conexión de Hello conserva su estado de degradado en Traffic Manager hasta que Hola sistema de supervisión realiza su próxima comprobación de mantenimiento.
10. **Reanuda el tráfico tooservice**. El Administrador de tráfico envía una solicitud GET y recibe una respuesta de estado 200 - Correcto. servicio de Hello ha devuelto el estado correcto de tooa. se actualizan los servidores de nombres del Administrador de tráfico de Hola e inician toohand el nombre DNS del servicio de hello en las respuestas DNS. Tráfico devuelve el punto de conexión de toohello como respuestas almacenadas en caché de DNS que devuelven otros puntos de conexión expiren y, como las conexiones existentes se finalizan los puntos de conexión tooother.

    > [!NOTE]
    > Porque Traffic Manager funciona en el nivel de DNS de hello, no se puede influir en el extremo de tooany de conexiones existente. Cuando dirige el tráfico entre los puntos de conexión (ya sea por la configuración de perfil cambiados o durante la conmutación por error o conmutación por recuperación), Administrador de tráfico dirige nuevos puntos de conexión de tooavailable de conexiones. Sin embargo, otros puntos de conexión podrían seguir tooreceive tráfico a través de las conexiones existentes hasta que terminen las sesiones. tooenable toodrain de tráfico de las conexiones existentes, las aplicaciones deben limitar Hola de duración de la sesión utilizado con cada punto de conexión.

## <a name="traffic-routing-methods"></a>Métodos de enrutamiento del tráfico

Cuando un punto de conexión tiene un estado degradado, ya no se devuelve en las consultas de tooDNS de respuesta. En su lugar, se elige y se devuelve un punto de conexión alternativo. el método de enrutamiento del tráfico de Hello configurado en el perfil de hello determina cómo se elige el punto de conexión alternativo Hola.

* **Prioridad**. Los puntos de conexión forman una lista clasificada en orden de prioridad. Hola primer punto de conexión disponible en la lista de hello siempre se devuelve. Si se degrada un estado de punto de conexión, se devuelve el punto de conexión disponible Hola siguiente.
* **Ponderado**. Cualquier punto de conexión disponible se elige de forma aleatoria en función de sus pesos asignados y Hola pesos de hello otros puntos de conexión disponibles.
* **Rendimiento**. usuario de Hello extremo más cercano toohello final se devuelve. Si ese punto de conexión no está disponible, un punto de conexión se elige aleatoriamente de Hola a todos los otros puntos de conexión disponibles. Elegir un punto de conexión aleatorio, evita un error en cascada que puede producirse al extremo más cercano Hola deja de estar sobrecargado. Puede configurar planes de conmutación por error alternativos para el enrutamiento del tráfico de rendimiento mediante los [perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Geográfico**. punto de conexión de Hello asignado ubicación geográfica del hello tooserve basado en solicitudes de consulta de Hola que IP se devuelve. Si ese punto de conexión no está disponible, otro punto de conexión no estará seleccionado toofailover, puesto que una ubicación geográfica puede ser el extremo de tooone sólo asignadas en un perfil (más detalles se encuentran en hello [preguntas más frecuentes sobre](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Como práctica recomendada, al usar el enrutamiento geográfico, se recomiendan a los clientes perfiles de Traffic Manager toouse anidada con más de un extremo como extremos de Hola de perfil de Hola.

Para más información, consulte [Métodos de enrutamiento del Administrador de tráfico](traffic-manager-routing-methods.md).

> [!NOTE]
> El comportamiento de enrutamiento del tráfico de toonormal de una excepción se produce cuando todos los extremos pueden tengan un estado degradado. Hace que el Administrador de tráfico un "esfuerzo" intente y *responde como si todos los puntos de conexión de estado de degradado Hola están realmente en un estado en línea*. Este comportamiento es preferible toohello alternativa, que podría ser toonot devolver cualquier extremo de hello respuesta DNS. No se supervisan los puntos de conexión con el estado Detenido o Deshabilitado, por lo tanto, no se consideran aptos para el tráfico.
>
> Esta condición normalmente se debe a una configuración incorrecta del servicio de hello, como:
>
> * Una lista de control de acceso [ACL] bloquear las comprobaciones de mantenimiento de hello Traffic Manager.
> * Una configuración incorrecta de hello puerto o protocolo Hola perfil del Administrador de tráfico de supervisión.
>
> Hello consecuencia de este comportamiento es que si las comprobaciones de mantenimiento de Traffic Manager no están configuradas correctamente, podría parecer de enrutamiento como si fuesen Traffic Manager del tráfico de hello *es* funciona correctamente. En cambio, en este caso, la conmutación por error del punto de conexión no se puede producir, lo que afecta a la disponibilidad general de la aplicación. Es importante toocheck que el perfil de hello muestra un estado en línea, no en un estado degradado. Un estado en línea indica que Hola Traffic Manager comprobaciones de mantenimiento funcionan del modo esperado.

Para obtener más información sobre la solución de problemas de comprobaciones se estado erróneas, consulte [Solución de problemas de estado degradado en Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Pasos siguientes

Aprenda [cómo funciona el Administrador de tráfico](traffic-manager-how-traffic-manager-works.md)

Obtener más información sobre hello [métodos de enrutamiento del tráfico](traffic-manager-routing-methods.md) compatible con el Administrador de tráfico

Obtenga información acerca de cómo demasiado[crear un perfil de Traffic Manager](traffic-manager-manage-profiles.md)

[Solución de problemas de estado degradado en el Administrador de tráfico de Azure](traffic-manager-troubleshooting-degraded.md)
