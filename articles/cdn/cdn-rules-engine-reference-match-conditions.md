---
title: las condiciones de coincidencia de motor de reglas de aaaAzure CDN | Documentos de Microsoft
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
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Condiciones de coincidencia del motor de reglas de la red CDN de Azure
Este tema enumera una descripción detallada de Hola condiciones disponibles de coincidencia del red de entrega de contenido (CDN) para Azure [motor de reglas de](cdn-rules-engine.md).

segunda parte de una regla de Hello es la condición de coincidencia de Hola. Una condición de coincidencia identifica tipos específicos de solicitudes para los que se ejecutará un conjunto de características.

Por ejemplo, es posible que las solicitudes de toofilter utilizado para el contenido en una ubicación concreta, las solicitudes que se genera a partir de una dirección IP o el país determinado, o información de encabezado.

## <a name="always"></a>Siempre

Hello condición de coincidencia siempre es diseñada tooapply establecer un valor predeterminado de las solicitudes de tooall de características.

## <a name="device"></a>Dispositivo

condición de coincidencia de dispositivo de Hello identifica las solicitudes realizadas desde un dispositivo móvil en función de sus propiedades.  La detección de dispositivos móviles se realiza a través de [WURFL](http://wurfl.sourceforge.net/).  A continuación se enumeran las funcionalidades de WURFL y sus variables de motor de reglas de red CDN.

> [!NOTE] 
> variables de Hello siguientes se admiten en hello **modificar el encabezado de solicitud de cliente** y **modificar encabezado de respuesta de cliente** características.

Capacidad | Variable | Descripción | Valores de ejemplo
-----------|----------|-------------|----------------
Nombre de la marca | %{wurfl_cap_brand_name} | Una cadena que indica el nombre de la marca de hello de dispositivo de Hola. | Samsung
Sistema operativo del dispositivo | %{wurfl_cap_device_os} | Una cadena que indica el sistema operativo de hello instalada en el dispositivo de Hola. | IOS
Versión del sistema operativo del dispositivo | %{wurfl_cap_device_os_version} | Una cadena que indica el número de versión de Hola de sistema operativo instalado en el dispositivo de Hola Hola. | 1.0.1
Orientación dual | %{wurfl_cap_dual_orientation} | Un valor booleano que indica si el dispositivo de hello admite orientación dual. | true
DTD preferido de HTML | %{wurfl_cap_html_preferred_dtd} | Una cadena que indica la definición de tipo del dispositivo móvil de hello preferido de documento (DTD) para el contenido HTML. | Ninguna<br/>xhtml_basic<br/>html5
Imagen de inclusión | %{wurfl_cap_image_inlining} | Un valor booleano que indica si el dispositivo de hello admite Base64 codificado imágenes. | false
Es Android | %{wurfl_vcap_is_android} | Un valor booleano que indica si el dispositivo de hello usa Hola SO Android. | true
Es IOS | %{wurfl_vcap_is_ios} | Un valor booleano que indica si el dispositivo de hello usa iOS. | false
Es Smart TV | %{wurfl_cap_is_smarttv} | Un valor booleano que indica si el dispositivo de hello es un Televisor inteligente. | false
Es smartphone | %{wurfl_vcap_is_smartphone} | Un valor booleano que indica si el dispositivo de hello es un smartphone. | true
Es tablet | %{wurfl_cap_is_tablet} | Un valor booleano que indica si el dispositivo de hello es una tableta. Esta es una descripción independiente del SO. | true
Es dispositivo inalámbrico | %{wurfl_cap_is_wireless_device} | Un valor booleano que indica si el dispositivo de Hola se considera un dispositivo inalámbrico. | true
Nombre de marca | %{wurfl_cap_marketing_name} | Una cadena que indica el nombre de marketing del dispositivo de Hola. | BlackBerry 8100 Pearl
Explorador móvil | %{wurfl_cap_mobile_browser} | Una cadena que indica el Explorador de hello usa contenido toorequest desde dispositivo Hola. | Chrome
Versión del explorador móvil | %{wurfl_cap_mobile_browser_version} | Una cadena que indica la versión de Hola del explorador de hello usa contenido toorequest desde dispositivo Hola. | 31
Nombre del modelo | %{wurfl_cap_model_name} | Una cadena que indica el nombre del modelo del dispositivo de Hola. | s3
Descarga progresiva | %{wurfl_cap_progressive_download} | Un valor booleano que indica si el dispositivo de hello compatible con la reproducción de Hola de audio/vídeo mientras todavía se está descargando. | true
Fecha de lanzamiento | %{wurfl_cap_release_date} | Una cadena que indica el año de Hola y el mes en qué Hola dispositivo era agrega base de datos de toohello WURFL.<br/><br/>Formato: `yyyy_mm` | 2013_december
Altura de resolución | %{wurfl_cap_resolution_height} | Un entero que indica el alto del dispositivo de hello en píxeles. | 768
Anchura de resolución | %{wurfl_cap_resolution_width} | Un entero que indica el ancho del dispositivo de hello en píxeles. | 1024


## <a name="location"></a>Ubicación

Estos coinciden con las condiciones se trata de solicitudes de tooidentify diseñado basadas en la ubicación del solicitante de Hola.

Nombre | Propósito
-----|--------
Número de sistema autónomo (AS) | Identifica solicitudes que se originan en una red determinada.
País | Identifica las solicitudes que se originan en hello especificado países.


## <a name="origin"></a>Origen

Estos coinciden con las condiciones se trata de solicitudes de tooidentify diseñada que tooCDN de punto de almacenamiento o un servidor de origen del cliente.

Nombre | Propósito
-----|--------
Origen de red CDN | Identifica solicitudes de contenido almacenado en el almacenamiento de CDN.
Origen de cliente | Identifica solicitudes de contenido almacenado en el servidor de origen de un cliente específico.


## <a name="request"></a>Solicitud

Estos coinciden con las condiciones son las solicitudes de tooidentify diseñado basadas en sus propiedades.

Nombre | Propósito
-----|--------
Dirección IP de cliente | Identifica solicitudes que se originan en una dirección IP determinada.
Parámetro de cookie | Comprobaciones de Hola cookies asociadas con cada solicitud de hello especificado valor.
Regex de parámetro de cookie | Comprueba las cookies de hello asociadas a cada solicitud de hello especificado expresión regular.
Cname perimetral | Identifica las solicitudes que señalan tooa específico borde CNAME.
Dominio de referencia | Identifica las solicitudes que se hace referencia desde Hola especificado hostname(s).
Literal de encabezado de solicitud | Identifica las solicitudes que contengan Hola especificado tooa de conjunto de encabezado especificado de valores.
Regex de encabezado de solicitud | Identifica las solicitudes que contengan Hola especificado valor del encabezado set tooa que coincide con hello especifica la expresión regular.
Carácter comodín de encabezado de solicitud | Identifica las solicitudes que contengan Hola especificado encabezado establece valor de tooa que coincide con el patrón especificado de Hola.
Método de solicitud | Identifica solicitudes por su método HTTP.
Esquema de solicitud | Identifica solicitudes por su protocolo HTTP.

## <a name="url"></a>URL

Estos coinciden con las condiciones son las solicitudes de tooidentify diseñado basándose en sus direcciones URL.

Nombre | Propósito
-----|--------
Directorio de ruta de acceso URL | Identifica solicitudes por su ruta de acceso relativa.
Extensión de ruta de acceso URL | Identifica solicitudes por su extensión de nombre de archivo.
Nombre de archivo de ruta de acceso URL | Identifica solicitudes por su nombre de archivo.
Literal de ruta de acceso URL | Compara una solicitud de ruta de acceso relativa toohello especificado del valor.
Regex de ruta de acceso URL | Compara una solicitud de ruta de acceso relativa toohello especificadas expresión regular.
Carácter comodín de ruta de acceso URL | Compara el patrón especificado de toohello de ruta de acceso relativa de la solicitud.
Literal de consulta de dirección URL | Compara una solicitud toohello de cadena de consulta especificado del valor.
Parámetro de consulta de dirección URL | Identifica las solicitudes que contienen la consulta especificada Hola parámetro de cadena de establece el valor de tooa que coincide con un patrón especificado.
Regex de consulta de dirección URL | Identifica las solicitudes que contienen la consulta especificada Hola parámetro de cadena de establece el valor de tooa que coincide con una expresión regular especificada.
Carácter comodín de consulta de dirección URL | Hola compara especifica valores de cadena de consulta de la solicitud de saludo.


## <a name="next-steps"></a>Pasos siguientes
* [Información general de la red CDN de Azure](cdn-overview.md)
* [Referencia del motor de reglas](cdn-rules-engine-reference.md)
* [Expresiones condicionales del motor de reglas](cdn-rules-engine-reference-conditional-expressions.md)
* [Funciones del motor de reglas](cdn-rules-engine-reference-features.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)

