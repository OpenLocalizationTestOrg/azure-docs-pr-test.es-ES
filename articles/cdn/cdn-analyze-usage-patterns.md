---
title: patrones de uso de CDN de Azure aaaAnalyze | Documentos de Microsoft
description: "Puede ver los patrones de uso de la red CDN mediante Hola después de informes: ancho de banda, datos transferidos, aciertos, Estados de memoria caché, frecuencia de aciertos de caché, datos transferidos a IPV4/IPV6."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Análisis de patrones de uso de la red CDN de Azure

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Guía de Hola a continuación recorre Hola pasos tooview Hola core informes mediante el portal de administración de hello Verizon perfiles de. También puede exportar toostorage de datos de análisis de núcleo, centro de eventos o análisis de registros (oms) para los perfiles Verizon y Akamai [a través del portal de azure hello](cdn-log-analysis.md).

Puede ver los patrones de uso de la red CDN mediante Hola después de informes:

* Ancho de banda
* Datos transferidos
* Aciertos
* Estados de la memoria caché
* Frecuencia de aciertos de caché
* Datos de IPV4/IPV6 transferidos

## <a name="accessing-core-reports"></a>Acceso a informes básicos
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **informes principales** ventana flotante.  Haga clic en informe de hello deseado en el menú de Hola.
   
    ![Portal de administración de la red CDN - menú Core Reports (Informes básicos)](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Ancho de banda
informe de ancho de banda de Hello consta de una tabla de gráfico y los datos que indican el uso de ancho de banda de Hola para HTTP y HTTPS a través de un período de tiempo determinado. Puede ver el uso de ancho de banda de Hola a través de un POP determinado o todos los POP de CDN. Esto permite tooview Hola tráfico alcanza su máximo y distribución a través de CDN se extrae en Mbps.

* Seleccione el tráfico de todos los nodos de borde toosee en todos los nodos o elija un región o un nodo específico de la lista desplegable de Hola.
* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc. o escribir las fechas personalizadas, haga clic en "Ir" toomake que se actualiza la selección.
* Puede exportar y datos de Hola de descarga, haga clic en hello excel icono hoja situada junto a demasiado "go".

informe de Hola se actualiza cada 5 minutos.

![Informe Ancho de banda](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Datos transferidos
Este informe se compone de una tabla de gráfico y los datos que indican el uso de tráfico de Hola para HTTP y HTTPS a través de un período de tiempo determinado. Puede ver el uso de tráfico de Hola a través de un POP determinado o todos los POP de CDN. Esto permite tooview Hola tráfico alcanza su máximo y distribución a través de CDN se extrae en GB.

* Seleccione el tráfico de todos los nodos de borde toosee de todas las notas o elija un región o un nodo específico de la lista desplegable de Hola.
* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc. o escribir las fechas personalizadas, haga clic en "Ir" toomake que se actualiza la selección.
* Puede exportar y datos de Hola de descarga, haga clic en hello excel icono hoja situada junto a demasiado "go".

informe de Hola se actualiza cada 5 minutos.

![Informe Datos transferidos](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Aciertos (códigos de estado)
Este informe describe la distribución de Hola de códigos de estado de solicitud para su contenido. Todas las solicitudes de contenido generarán un código de estado HTTP. código de estado de Hello describe cómo borde POP controla la solicitud de saludo. Por ejemplo, códigos de estado de 2xx indican que Hola solicitud recibió correctamente el servicio a tooa cliente, mientras que un código de estado 4xx indica que se produjo un error. Para obtener más detalles sobre el código de estado HTTP, consulte [códigos de estado](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc. o escribir las fechas personalizadas, haga clic en "Ir" toomake que se actualiza la selección.
* Puede exportar y datos de Hola de descarga, haga clic en hello excel hoja situada junto a demasiado "go".

![Informe Aciertos](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Estados de la memoria caché
Este informe describe la distribución de Hola de aciertos de caché y errores de caché de solicitud de cliente. Puesto que el rendimiento más rápido de hello procede de aciertos de caché, puede optimizar velocidades de entrega de datos por minimizar errores de caché y de aciertos de caché expirados. Errores de caché pueden reducirse mediante la configuración de su tooavoid de servidor de origen asignación de encabezados de respuesta "no-cache" y evitando la cadena de consulta el almacenamiento en caché excepto donde estrictamente necesaria, evitando los códigos de respuesta no almacenable en caché. Caducado aciertos pueden evitarse mediante la realización max-age de un recurso como posibles toominimize Hola número del servidor de origen de toohello las solicitudes de caché.

![Informe Estados de la memoria caché](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Los principales estados de la memoria caché incluyen:
* TCP_HIT: servido desde el extremo. objeto Hola estaba en caché y no había superado su max-age.
* TCP_MISS: servido desde el origen. objeto Hello no estaba en caché y respuesta Hola era tooorigin atrás.
* TCP_EXPIRED _MISS: servido desde el origen después de la revalidación con el origen. objeto de Hello estaba en caché pero haber superado su max-age. Dio como resultado una validación con el origen de objeto de caché de Hola que será reemplazada por una nueva respuesta de origen.
* TCP_EXPIRED _HIT: servido desde el extremo después de la revalidación con el origen. objeto de Hello estaba en caché pero haber superado su max-age. Dio como resultado una validación con el servidor de origen de hello en el objeto de caché de hello está sin modificar.
* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc. o escribir las fechas personalizadas, haga clic en "Ir" toomake que se actualiza la selección.
* Puede exportar y datos de Hola de descarga, haga clic en hello excel icono hoja situada junto a demasiado "go".

### <a name="full-list-of-cache-statuses"></a>Lista completa de los estados de la memoria caché
* TCP_HIT - se comunica este estado cuando una solicitud se sirve directamente desde el cliente de toohello Hola POP. Un activo inmediatamente provienen de un POP cuando se almacena en caché en cliente de toohello más cercano de hello POP y tiene una válida time-to-live o TTL. TTL viene determinada por hello después de encabezados de respuesta:
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * Expira
* TCP_MISS - este estado indica que no se encontró una versión almacenada en caché del recurso solicitado hello en cliente de toohello de hello POP más cercano. activos de Hola se solicitará desde un servidor de origen o en un servidor del icono de escudo de origen. Si el servidor de origen de Hola u Hola origen escudo devuelve un recurso, se atienden a toohello cliente y almacenan en caché en el cliente de Hola y el servidor de borde de Hola. De lo contrario, se devolverá un código de estado que no sea 200 (p. ej., 403 Prohibido, 404 no encontrado, etc.).
* TCP_EXPIRED _HIT - este estado se establece cuando se realizó una solicitud destinados a un recurso con un TTL expirado, por ejemplo, cuando ha expirado la vigencia máxima del recurso de hello, el servicio directamente desde el cliente de toohello Hola POP.
  
    Una solicitud caducada normalmente como resultado en un servidor de origen revalidación toohello de solicitud. En orden para un toooccur _HIT TCP_EXPIRED, el servidor de origen de hello debe indicar que no existe una versión más reciente del recurso de Hola. Este tipo de situación normalmente actualizará los encabezados Cache-Control y Expires de dicho recurso.
* TCP_EXPIRED _MISS - se notifica este estado cuando una versión más reciente de un recurso almacenado en caché expirado se sirve desde el cliente de toohello Hola POP. Esto se produce cuando ha expirado Hola TTL para un activo en caché (p. ej., caducado max-age) y servidor de origen de hello devuelve una versión más reciente de dicho activo. Esta nueva versión del recurso de Hola se servirá a toohello cliente en lugar de la versión almacenada en caché de Hola. Además, se almacenarán en el servidor perimetral de Hola y el cliente de Hola.
* CONFIG_NOCACHE - este estado indica que una configuración específica del cliente en el borde POP puede asset Hola está almacenando en caché.
* NONE: este estado indica que no se realizó una comprobación de actualización del contenido de la memoria caché.
* TCP_ CLIENT_REFRESH _MISS - este estado se notifica cuando un cliente HTTP (p. ej., explorador) fuerza un tooretrieve borde POP una nueva versión de un recurso obsoleto del servidor de origen de Hola.
  
    De forma predeterminada, nuestros servidores impedir que un cliente HTTP forzar nuestro tooretrieve de servidores de borde una nueva versión del recurso de Hola desde el servidor de origen de Hola.
* TCP_ PARTIAL_HIT: este estado se comunica cuando una solicitud de intervalo de bytes da como resultado un acierto para un recurso almacenado parcialmente en caché. Hola solicitó el intervalo de bytes inmediatamente provienen de cliente de hello POP toohello.
* ALMACENABLE - este estado se notifica cuando un recurso Cache-Control y encabezados Expires indican que no se debe guardar en un POP o cliente hello HTTP. Estos tipos de solicitudes se atienden desde el servidor de origen de Hola

## <a name="cache-hit-ratio"></a>Frecuencia de aciertos de caché
Este informe indica el porcentaje de Hola de solicitudes en caché que se pueda servir directamente desde la memoria caché.

informe de Hello proporciona Hola detalles siguientes:

* Hola solicitado se almacenó en caché contenido de solicitante de toohello de hello POP más cercano.
* solicitud de saludo se realizó el servicio directamente desde el perímetro de Hola de nuestra red.
* solicitud de Hello no era necesario revalidación con servidor de origen de Hola.

informe de Hello no incluye:

* Solicitudes que se haya denegado debido a las opciones de filtrado toocountry.
* Solicitudes de recursos cuyos encabezados indican que no se deben almacenar en caché. Por ejemplo, los encabezados Cache-Control: private, Cache-Control: no-cache o Pragma: no-cache impedirán que un recurso se almacene en caché.
* Solicitudes de intervalo de bytes para contenido almacenado parcialmente en caché.

Hola fórmula es: (TCP_ ACIERTO / (ACIERTOS de TCP_ + TCP_MISS)) * 100

* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc. o escribir las fechas personalizadas, haga clic en "Ir" toomake que se actualiza la selección.
* Puede exportar y datos de Hola de descarga, haga clic en hello excel icono hoja situada junto a demasiado "go".

![Informe Frecuencia de aciertos de caché](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Datos de IPV4/IPV6 transferidos
Este informe muestra la distribución de uso de tráfico de hello en IPV4 frente a IPV6.

![Datos de IPV4/IPV6 transferidos](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Seleccionar datos de tooview de intervalo de fecha de hoy o esta semana/este mes, etc., o escribir las fechas personalizadas.
* A continuación, haga clic en "Ir" toomake que se actualiza la selección.

## <a name="considerations"></a>Consideraciones
Informes sólo pueden generarse en hello últimos 18 meses.

