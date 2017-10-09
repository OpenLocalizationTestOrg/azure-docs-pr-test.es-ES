---
title: "aaaHow tooUse Hola API de interacción en iOS"
description: "IOS más reciente SDK - cómo tooUse Hola API de interacción en iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>¿Cómo tooUse Hola API de interacción en iOS
Este documento es un complemento toohello cómo tooIntegrate interacción en iOS: proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.

Tenga en cuenta que si sólo desea interacción tooreport sesiones, actividades, bloqueos y obtener información técnica, de la aplicación hello más sencillo cierto es toomake todos personalizado `UIViewController` objetos heredan de hello correspondiente `EngagementViewController` (clase) .

Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementViewController` clases, deberá toouse Hola API de contratación.

Hello interacción API proporcionada por hello `EngagementAgent` clase. Se puede recuperar una instancia de esta clase que realiza la llamada hello `[EngagementAgent shared]` método estático (tenga en cuenta que hello `EngagementAgent` objeto devuelto es un singleton).

Antes de que las llamadas de API, hello `EngagementAgent` objeto debe inicializarse mediante una llamada a método hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Conceptos de Engagement
Hello partes siguientes refinar Hola comunes [Mobile Engagement conceptos](mobile-engagement-concepts.md) para la plataforma de iOS de Hola.

### <a name="session-and-activity"></a>`Session` y `Activity`
Un *actividad* suele estar asociado a una pantalla de la aplicación hello, que es hello toosay *actividad* se inicia cuando la pantalla de bienvenida se muestra y se detiene cuando se cierra la pantalla de bienvenida: se trata de hello caso en el que Hello Engagement SDK integrado utilizando hello `EngagementViewController` clases.

Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola. Esto permite toosplit una pantalla determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta pantalla (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta pantalla).

## <a name="reporting-activities"></a>Informes sobre actividades
### <a name="user-starts-a-new-activity"></a>El usuario inicia una nueva actividad
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Necesita toocall `startActivity()` cambia cada actividad de usuario de hello de tiempo. Hola primera llamada toothis función inicia una nueva sesión de usuario.

### <a name="user-ends-his-current-activity"></a>El usuario finaliza su actividad actual
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Debería **nunca** llame a esta función por sí mismo, excepto si desea toosplit un uso de la aplicación en varias sesiones: una llamada de función toothis finalizaría Hola actual sesión inmediatamente, por lo tanto, una llamada subsiguiente demasiado`startActivity()`podría iniciar una sesión de nuevo. Esta función se invoca automáticamente por hello SDK cuando se cierra la aplicación.
> 
> 

## <a name="reporting-events"></a>Informes de eventos
### <a name="session-events"></a>Eventos de sesión
Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.

**Ejemplo sin datos adicionales:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Ejemplo con datos adicionales:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Eventos independientes
Eventos toosession contrarias, independiente pueden utilizarse fuera de contexto de Hola de una sesión.

**Ejemplo:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Informes de errores
### <a name="session-errors"></a>Errores de sesión
Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.

**Ejemplo:**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Errores independientes
Toosession contrarias errores, errores de independientes se pueden utilizar fuera de contexto de Hola de una sesión.

**Ejemplo:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Informes de trabajos
**Ejemplo:**

Suponga que desea tooreport Hola que dure el proceso de inicio de sesión:

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Informe de errores durante un trabajo
Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.

**Ejemplo:**

Suponga que desea tooreport un error durante el proceso de inicio de sesión:

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>Eventos durante un trabajo
Pueden tooa relacionado ejecutando el trabajo en lugar de eventos relacionados con la sesión del usuario actual toohello.

**Ejemplo:**

Supongamos que tenemos una red social, y utilizamos un trabajo tooreport Hola tiempo total durante qué Hola usuario está conectado toohello server. usuario de Hello puede recibir mensajes de sus amigos, se trata de un evento de trabajo.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Parámetros adicionales
Pueden ser datos arbitrarios tooevents adjunto, errores, las actividades y trabajos.

Estos datos pueden estructurarse, utilizan la clase de NSDictionary de iOS.

Tenga en cuenta que los extras pueden contener `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` u otras `NSDictionary` instancias.

> [!NOTE]
> Hello adicional parámetro se serializa en JSON. Si desea toopass distintos objetos que hello las descritas anteriormente, debe implementar Hola siguiendo el método en la clase:
> 
> -(NSString*)JSONRepresentation;
> 
> método Hello debe devolver la representación JSON del objeto.
> 
> 

### <a name="example"></a>Ejemplo
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Límites
#### <a name="keys"></a>simétricas
Cada clave de hello `NSDictionary` debe coincidir con la siguiente expresión regular de Hola:

`^[a-zA-Z][a-zA-Z_0-9]*`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Extras se limitan demasiado**1024** caracteres por llamada (una vez codificados en JSON por agente de interacción de hello).

Hola ejemplo anterior, Hola JSON enviado toohello server es 58 caracteres:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Información de la aplicación de informes
Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de aplicación) con hello `sendAppInfo:` función.

Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.

Como extras de eventos, hello `NSDictionary` clase es tooabstract usa información de la aplicación, tenga en cuenta que las matrices o diccionarios secundarios se tratará como cadenas sin formato (con la serialización de JSON).

**Ejemplo:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Límites
#### <a name="keys"></a>simétricas
Cada clave de hello `NSDictionary` debe coincidir con la siguiente expresión regular de Hola:

`^[a-zA-Z][a-zA-Z_0-9]*`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Información de la aplicación se limitan demasiado**1024** caracteres por llamada (una vez codificados en JSON por agente de interacción de hello).

Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:

    {"birthdate":"1983-12-07","gender":"female"}
