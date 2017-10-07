---
title: aaaTemplates
description: En este tema se explican las plantillas para los Centros de notificaciones de Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Plantillas
## <a name="overview"></a>Información general
Las plantillas permiten un cliente toospecify Hola exacta formato de aplicación de notificaciones de Hola que desee tooreceive. Mediante plantillas, una aplicación puede obtener distintas ventajas, incluidos Hola siguientes:

* Un back-end independiente de la plataforma
* Notificaciones personalizadas
* Independencia de la versión del cliente
* Localización sencilla

Esta sección proporciona dos ejemplos detallados de cómo toouse plantillas toosend independiente de la plataforma las notificaciones de todos los dispositivos de destino a través de plataformas y toopersonalize difusión dispositivo tooeach de notificación.

## <a name="using-templates-cross-platform"></a>Uso de plantillas multiplataforma
notificaciones de inserción de toosend de manera estándar de Hello es toosend, para cada notificación que es toobe envía, un servicios de notificación de tooplatform carga concreto (WNS, APNS). Por ejemplo, una alerta tooAPNS, toosend carga Hola es un objeto Json de hello siguiente forma:

    {"aps": {"alert" : "Hello!" }}

toosend un mensaje de notificación del sistema similar en una aplicación Windows Store, carga XML de hello es como sigue:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

Puede crear cargas similares para plataformas MPNS (Windows Phone) y GCM (Android).

Este requisito fuerza Hola aplicación back-end tooproduce diferentes cargas para cada plataforma y eficazmente hace responsable de la parte de la capa de presentación de Hola de aplicación hello Hola back-end. Algunos problemas incluye diseños gráficos y de localización (especialmente para las aplicaciones de la Tienda Windows que incluyen notificaciones para varios tipos de iconos).

característica de plantilla de centros de notificaciones de Hello permite que una aplicación toocreate especial registros de cliente, llama a los registros de plantilla, que incluyen, además de toohello conjunto de etiquetas, una plantilla. característica de plantilla de centros de notificaciones de Hello permite dispositivos cliente aplicación tooassociate con plantillas si está trabajando con las instalaciones (opción preferidas) o registros. Dados Hola anteriores ejemplos de carga, hello únicamente información de independiente de la plataforma es Hola real mensaje de alerta (Hola). Una plantilla es un conjunto de instrucciones para el centro de notificaciones de hello en cómo tooformat un independiente de la plataforma mensaje para el registro de hello de esa aplicación de cliente específico. En el anterior ejemplo de Hola, mensaje de bienvenida de plataforma independiente es una propiedad única: **mensaje = Hello!**.

Hola siguiente imagen muestra hello por encima de proceso:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

plantilla de Hello para el registro de aplicación de cliente de iOS de hello es como sigue:

    {"aps": {"alert": "$(message)"}}

Hola plantilla correspondiente para la aplicación de cliente de la tienda Windows hello es:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Tenga en cuenta que Hola real del mensaje se sustituye por la expresión de hello $(mensaje). Esta expresión indica Hola centro de notificaciones, cada vez que envía un mensaje toothis registro determinado, un mensaje que sigue a él y los conmutadores de valor común de hello toobuild.

Si está trabajando con el modelo de instalación, clave de la instalación "plantillas" hello contiene JSON de varias plantillas. Si está trabajando con el modelo de registro, aplicación de cliente de hello puede crear de la varios registros en orden toouse varias plantillas; Por ejemplo, una plantilla para mensajes de alerta y una plantilla para las actualizaciones. Las aplicaciones cliente también pueden combinar los registros nativos (registros sin plantilla) y los registros de plantilla.

Hola centro de notificaciones envía una notificación para cada plantilla sin tener en cuenta si pertenecen toohello misma aplicación de cliente. Este comportamiento puede ser notificaciones de independiente de la plataforma tootranslate usados en notificaciones más. Por ejemplo, hello toohello de mensaje independiente de plataforma mismo que centro de notificaciones se pueden traducir sin problemas en una alerta de notificación del sistema y una actualización del icono, sin necesidad de Hola toobe de back-end consciente de ello. Tenga en cuenta que algunas plataformas (por ejemplo, iOS) pueden contraer varias toohello notificaciones mismo dispositivo si se envían en un breve período de tiempo.

## <a name="using-templates-for-personalization"></a>Uso de plantillas para personalización
Plantillas de toousing de otra ventaja es Hola capacidad toouse personalización de los centros de notificaciones tooperform por registro de notificaciones. Por ejemplo, considere la posibilidad de una aplicación del tiempo que muestra un icono con las condiciones meteorológicas de hello en una ubicación específica. Un usuario puede elegir entre grados Celsius o Fahrenheit, además de un pronóstico de un día o de cinco días. Mediante plantillas, cada instalación de la aplicación cliente puede registrar para formato Hola requerido (1 día Celsius, 1 día Fahrenheit, 5 días grados centígrados, 5 días Fahrenheit), y que Hola back-end envíe un mensaje único que contiene toda la información de hello necesario toofill los plantillas (por ejemplo, una cinco días previsión con grados Celsius y Fahrenheit).

plantilla de Hola Hola un día de previsión con grados centígrados temperaturas es como sigue:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

Hola mensaje enviado toohello centro de notificaciones contiene Hola todas las propiedades siguientes:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Mediante el uso de este patrón, Hola back-end sólo envía un mensaje único sin necesidad de opciones de personalización específicas de toostore para los usuarios de aplicación Hola. Hola siguiente muestra este escenario:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>¿Cómo tooregister plantillas
tooregister con plantillas mediante el modelo de instalación de hello (opción preferida) o hello modelo de registro, consulte [administración de registros](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Lenguaje de expresión de plantilla
Las plantillas son tooXML limitado o formatos de documento JSON. Además, solo puede ubicar expresiones en lugares específicos; por ejemplo, valores o atributos de nodo para XML, valores de propiedad de cadena para JSON.

Hello siguiente tabla muestra lenguaje Hola permitida en las plantillas:

| Expression | Descripción |
| --- | --- |
| $(prop) |Propiedad de evento de tooan de referencia con el nombre especificado de Hola. Los nombres de propiedad no distinguen mayúsculas de minúsculas. Esta expresión se resuelve en valor de texto de la propiedad de Hola o en una cadena vacía si no hay propiedad Hola. |
| $(prop, n) |Como anteriormente, pero hello se explícitamente texto se recorta en n caracteres, por ejemplo $(título, 20) recorta contenido Hola de propiedad de título de hello en 20 caracteres. |
| .(prop, n) |Como anteriormente, pero hello texto se utiliza como sufijo con tres puntos tal y como se recorta. tamaño total de Hola de hello recorta la cadena y sufijo hello no supere los n caracteres. . (cargo, 20) con una propiedad de entrada de "This is línea del título de Hola" da como resultado **este es el título de Hola...** |
| %(prop) |Too$(name) similar, salvo que los resultados del Hola está codificada por el URI. |
| #(prop) |Se usa en las plantillas JSON (por ejemplo, para plantillas de iOS y Android).<br><br>Esta función funciona exactamente igual Hola como $(prop) especificado anteriormente, excepto cuando se utilizan en las plantillas de JSON (por ejemplo, plantillas de Apple). En este caso, si esta función no está rodeada por "{','}" (por ejemplo, 'myJsonProperty': "#(name)"), y se evalúa como el número de tooa en formato de Javascript, por ejemplo, regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. ¿&#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, a continuación, Hola de salida JSON es un número.<br><br>Por ejemplo, ‘badge : ‘#(name)’ se convierte en ‘badge’ : 40 (y no ‘40‘). |
| ‘texto’ o “texto” |Un literal. Los literales contienen texto arbitrario encerrado entre comillas simples o dobles. |
| expr1 + expr2 |operador de concatenación de Hello combinar dos expresiones en una sola cadena. |

expresiones de Hello pueden ser cualquiera de hello anterior formularios.

Cuando se utiliza la concatenación, la expresión completa de Hola debe incluirse entre con {}. Por ejemplo, {$(prop) + ‘ - ’ + $(prop2)}. |

Por ejemplo, el siguiente hello no es una plantilla XML válida:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Como se explicó anteriormente, cuando se usa la concatenación, las expresiones deben ir entre llaves. Por ejemplo:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

