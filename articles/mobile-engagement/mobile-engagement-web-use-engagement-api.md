---
title: API del SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Usar hello Azure Mobile Engagement API en una aplicación web
Este documento es un documento de toohello de suma que le indica cómo demasiado[integrar Mobile Engagement en una aplicación web](mobile-engagement-web-integrate-engagement.md). Proporciona información detallada acerca de cómo toouse Hola API de Azure Mobile Engagement tooreport las estadísticas de la aplicación.

Hello API de Mobile Engagement proporciona hello `engagement.agent` objeto. Hola predeterminado SDK de Azure Mobile Engagement Web alias es `engagement`. Puede volver a definir este alias de configuración de SDK de Hola.

## <a name="mobile-engagement-concepts"></a>Conceptos de Mobile Engagement
Hello partes siguientes refinar comunes [conceptos de Mobile Engagement](mobile-engagement-concepts.md) de plataforma web de Hola.

### <a name="session-and-activity"></a>`Session` y `Activity`
Si el usuario de Hola permanece inactiva durante más de unos pocos segundos entre dos actividades, hello secuencia del usuario de actividades se divide en dos sesiones diferentes. Estos pocos segundos se denominan Hola tiempo de espera de sesión.

Si la aplicación web no declara final Hola de actividades de usuario por sí mismo (por Hola que realiza la llamada `engagement.agent.endActivity` función), servidor de Mobile Engagement Hola expira automáticamente Hola sesión de usuario en los tres minutos después de cerrar la página de aplicación Hola. Esto se denomina tiempo de espera de sesión de servidor de Hola.

### `Crash`
No se crean informes automatizados de excepciones de JavaScript no detectadas de forma predeterminada. Sin embargo, puede crear informes de bloqueos manualmente mediante el uso de hello `sendCrash` función (consulte la sección de hello en reporting bloqueos).

## <a name="reporting-activities"></a>Informes sobre actividades
Creación de informes sobre la actividad de usuario incluye cuando un usuario inicia una nueva actividad, y al usuario de hello finaliza la actividad actual de hello.

### <a name="user-starts-a-new-activity"></a>El usuario inicia una nueva actividad
    engagement.agent.startActivity("MyUserActivity");

Necesita toocall `startActivity()` cambia cada actividad de usuario de tiempo. Hola primera llamada toothis función inicia una nueva sesión de usuario.

### <a name="user-ends-hello-current-activity"></a>Usuario finaliza la actividad actual de hello
    engagement.agent.endActivity();

Necesita toocall `endActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad. Este modo, se informa hello Web SDK de Mobile Engagement que usuario Hola está inactivo y que la sesión de usuario de hello necesita toobe cerrado después de que expire el tiempo de espera de sesión de Hola. Si se llama a `startActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente se reanuda la sesión de Hola.

Porque no hay ninguna llamada confiable para cuando se cierra la ventana del navegador de hello, suele ser final de hello toocatch difíciles o imposibles de actividades de usuario dentro de un entorno web. ¿Por qué que se Hola Mobile Engagement server expira automáticamente sesión de usuario de hello en los tres minutos después de cerrar la página de aplicación Hola.

## <a name="reporting-events"></a>Informes de eventos
La creación de informes sobre eventos incluye los eventos de sesión y los eventos independientes.

### <a name="session-events"></a>Eventos de sesión
Eventos de sesión suelen ser las acciones de hello tooreport usado realizadas por un usuario durante la sesión de usuario de Hola.

**Ejemplo sin datos adicionales:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Ejemplo con datos adicionales:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Eventos independientes
A diferencia de los eventos de sesión, pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.

Por ello, utilice ``engagement.agent.sendEvent`` en lugar de ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Informes de errores
La creación de informes sobre errores incluye los errores de sesión y los errores independientes.

### <a name="session-errors"></a>Errores de sesión
Errores de sesión suelen ser errores de hello tooreport usado que tenga un impacto en el usuario de Hola durante la sesión de usuario de Hola.

**Ejemplo sin datos adicionales:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Ejemplo con datos adicionales:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Errores independientes
A diferencia de los errores de la sesión, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.

Por ello, utilice `engagement.agent.sendError` en lugar de `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Informes de trabajos
La creación de informes sobre trabajos incluye la notificación de errores y eventos que se producen durante un trabajo y la notificación de bloqueos.

**Ejemplo:**

Si desea toomonitor una solicitud AJAX, utilizaría Hola siguiente:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Informes de errores durante un trabajo
Errores pueden ser tooa relacionado ejecutando el trabajo en lugar de toohello sesión del usuario actual.

**Ejemplo:**

Si desea que un error si una solicitud AJAX tooreport produce un error:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Informes de eventos durante un trabajo
Los eventos pueden ser tooa relacionado ejecutando trabajo en lugar de la sesión del usuario actual toohello, gracias toohello `engagement.agent.sendJobEvent` función.

Esta función se comporta exactamente como `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Informes de bloqueos
Hola de uso `sendCrash` tooreport de función se bloquea de forma manual.

Hola `crashid` argumento es una cadena que identifica el tipo de saludo de bloqueo.
Hola `crash` argumento es normalmente el seguimiento de la pila de Hola de fallo de hello como una cadena.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Parámetros adicionales
Puede asociar el evento tooan de datos arbitrarios, error, actividad o el trabajo.

Hola datos pueden ser cualquier objeto JSON (pero no una matriz o tipo primitivo).

**Ejemplo:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>límites
Límites que se apliquen tooextra parámetros están en áreas de Hola de expresiones regulares para las claves, tipos de valor y tamaño.

#### <a name="keys"></a>simétricas
Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:

    ^[a-zA-Z][a-zA-Z_0-9]*

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="values"></a>Valores
Los valores son toostring limitado, el número y los tipos booleanos.

#### <a name="size"></a>Tamaño
Extras son too1 limitado, 024 caracteres por llamada (después de hello Web SDK de Mobile Engagement lo codifica en JSON).

## <a name="reporting-application-information"></a>Información de la aplicación de informes
Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de la aplicación) mediante el uso de hello `sendAppInfo()` función.

Tenga en cuenta que esta información se puede enviar de forma incremental. Solo Hola valor más reciente de una clave específica se mantendrán para un dispositivo específico.

Como eventos adicionales, puede usar cualquier información de aplicación de tooabstract de objeto JSON. Tenga en cuenta que las matrices o subobjetos se tratarán como cadenas sin formato (con la serialización de JSON).

**Ejemplo:**

Este es un ejemplo de código para el género del usuario que envía hello y fecha de nacimiento:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>límites
Son límites que se apliquen tooapplication información en las áreas de Hola de expresiones regulares para las claves y el tamaño.

#### <a name="keys"></a>simétricas
Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:

    ^[a-zA-Z][a-zA-Z_0-9]*

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Información de la aplicación es too1 limitado, 024 caracteres por llamada (después de hello Web SDK de Mobile Engagement lo codifica en JSON).

En el anterior ejemplo de Hola, hello JSON enviadas toohello server es 44 caracteres:

    {"birthdate":"1983-12-07","gender":"female"}
