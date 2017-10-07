---
title: "conceptos de interacción de aaaMobile | Documentos de Microsoft"
description: Conceptos de Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Conceptos de Azure Mobile Engagement
Mobile Engagement define algunos conceptos comunes tooall admitida las plataformas. En este artículo se describen brevemente dichos conceptos.

Este artículo es un buen punto de partida si es nuevo tooMobile interacción. También la convierten seguro tooread Hola documentación toohello específico plataforma que usa, como perfeccionar los conceptos de hello descritos en este artículo con más detalles y ejemplos, así como posibles limitaciones.

## <a name="devices-and-users"></a>Dispositivos y usuarios
Mobile Engagement identifica a los usuarios mediante la generación de un identificador único para cada dispositivo, Este identificador se denomina identificador de dispositivo de hello (o `deviceid`). Se genera de forma que la ejecución de todas las aplicaciones de Hola mismo recurso compartido de dispositivo Hola mismo identificador de dispositivo.

Implícitamente, significa que Mobile Engagement considera que un dispositivo toobelong tooexactly un usuario y, por lo tanto, los usuarios y dispositivos son conceptos equivalente.

## <a name="sessions-and-activities"></a>Sesiones y actividades
Una sesión es un uso de la aplicación hello realizada por un usuario, de usuario en Hola Hola tiempo comenzará a utilizarla, hasta que se detiene de usuario de Hola.

Una actividad se muestra un uso de un elemento secundario determinado de aplicación Hola realizada por un usuario (suele ser una pantalla, pero puede ser cualquier cosa adecuado toohello aplicación).

Un usuario solo puede realizar una actividad a la vez.

Una actividad se identifica mediante un nombre (too64 limitado caracteres) y, opcionalmente, puede incrustar algunos datos adicionales (en el límite de Hola de 1024 bytes).

Las sesiones se calculan de forma automática desde la secuencia de Hola de las actividades realizadas por los usuarios. Inicia una sesión al usuario Hola su primera actividad inicia y se detiene cuando acabe su última actividad. Esto significa que una sesión no es necesario toobe explícitamente iniciaron o detuvieron inesperadamente. En cambio, las actividades se inician y detienen explícitamente. Si no se notifica ninguna actividad, tampoco se notifica ninguna sesión.

## <a name="events"></a>Eventos
Los eventos son acciones de instantánea de tooreport utilizado (por ejemplo, el botón presionado o artículos leídos por los usuarios).

Un evento puede ser relacionado toohello sesión actual, tooa ejecuta el trabajo, o puede ser un evento independiente.

Un evento se identifica mediante un nombre (too64 limitado caracteres) y, opcionalmente, puede incrustar algunos datos adicionales (en el límite de Hola de 1024 bytes).

## <a name="error"></a>Error
Errores son problemas de uso tooreport detectados correctamente la aplicación hello (por ejemplo, las acciones de usuario incorrectos o errores de llamadas a API).

Un error puede ser relacionado toohello sesión actual, tooa ejecuta el trabajo, o puede ser un error independiente.

Un error identificado por un nombre (too64 limitado caracteres) y, opcionalmente, puede incrustar algunos datos adicionales (en el límite de Hola de 1024 bytes).

## <a name="job"></a>Trabajo
Trabajos son acciones tooreport usados con una duración (al igual que la duración de las llamadas de API, Mostrar tiempo de anuncios, la duración de tareas en segundo plano o la duración de las acciones del usuario).

Un trabajo no es sesión tooa relacionados, porque se pueden realizar una tarea en segundo plano de hello, sin ninguna interacción del usuario.

Un trabajo se identifica mediante un nombre (too64 limitado caracteres) y, opcionalmente, puede incrustar algunos datos adicionales (en el límite de Hola de 1024 bytes).

## <a name="crash"></a>Bloqueo
Hola aplicación tooreport de SDK de Mobile Engagement bloquearse errores donde aplicación hello no detectados los problemas que se emiten bloqueos automáticamente.

## <a name="application-information"></a>Información de la aplicación
Información de la aplicación (o información de la aplicación) son usado tootag a los usuarios, es decir, tooassociate algunos usuarios de toohello de datos de una aplicación (Esto es similar tooweb las cookies, salvo que se almacena información de la aplicación en servidor hello en plataforma de Azure Mobile Engagement hello).

Mediante el uso de API del SDK de Mobile Engagement Hola o con la plataforma de Mobile Engagement Hola API de dispositivo, se puede registrar información de la aplicación.

Información de la aplicación es un dispositivo de tooa asociado del par de clave/valor. clave de Hello es nombre Hola de información de la aplicación hello (too64 limitado letras ASCII [a-zA-Z], [0-9] de números y caracteres de subrayado [_]). valor de Hello (too1024 limitado caracteres) puede ser cualquier cadena, entero, fecha (aaaa-MM-dd) o un valor booleano (true o false).

Dispositivo tooa asociado, dentro de los límites de hello definida por condiciones de precios de Mobile Engagement hello, pueden contener cualquier número de información de la aplicación. Para una clave determinada, Mobile Engagement solo realiza un seguimiento de conjunto de valor más reciente de hello (ningún historial). Establecer o cambiar valor Hola de una información de aplicación obliga a Mobile Engagement toore-evaluar criterios de audiencia que se establecen en esta aplicación información (si existe), lo que significa que esa información de la aplicación puede ser inserciones de tootrigger utilizado en tiempo real.

## <a name="extra-data"></a>Datos adicionales
Datos adicionales (o extras) son algunos datos arbitrarios que pueden ser tooevents adjunto, errores, las actividades y trabajos.

Extras se estructuran de forma similar tooJSON objetos: se realizan de un árbol de pares clave/valor. Las claves son letras de ASCII de too64 limitado [a-zA-Z], [0-9] de números y caracteres de subrayado [_]) y tamaño total de Hola de extras es limitado too1024 caracteres (una vez codificados en JSON por hello SDK de Mobile Engagement).

todo el árbol Hola de pares clave/valor se almacena como un objeto JSON. No obstante, solo nivel primera Hola de claves/valores está toobe descompuesto directamente accesible toosome avanzadas funciones como segmentos (por ejemplo, se puede definir fácilmente un segmento denominado "SciFi ventiladores" que está formado por todos los usuarios tener envía eventos de Hola de al menos 10 veces con el nombre "content_viewed" con hello extra clave "content_type" conjunto toohello valor "scifi" Hola último mes). Por lo tanto se recomienda toosend extras solo formadas listas simples de pares clave/valor con valores escalares (por ejemplo, cadenas, fechas, enteros o un valor booleano).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción al SDK de Windows Universal para Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Introducción al SDK de Windows Phone Silverlight para Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [SDK de iOS para Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [SDK de Android para Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

