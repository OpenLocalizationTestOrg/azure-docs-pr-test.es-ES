---
title: "aaaHow tooUse Hola API de interacción en Android"
description: "SDK de Android más reciente: cómo tooUse Hola API de interacción en Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>¿Cómo tooUse Hola API de interacción en Android
Este documento es un complemento toohello [opciones avanzadas Reporting para Android SDK de Mobile Engagement](mobile-engagement-android-advanced-reporting.md). Proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.

Tenga en cuenta que si sólo desea tooreport de interacción de su aplicación sesiones, actividades, se bloquea y obtener información técnica, a continuación, hello manera más sencilla de toomake todas la `Activity` subclases heredan de hello correspondiente `EngagementActivity` clase.

Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementActivity` clases, deberá toouse Hola API de contratación.

Hello interacción API proporcionada por hello `EngagementAgent` clase. Se puede recuperar una instancia de esta clase que realiza la llamada hello `EngagementAgent.getInstance(Context)` método estático (tenga en cuenta que hello `EngagementAgent` objeto devuelto es un singleton).

## <a name="engagement-concepts"></a>Conceptos de Engagement
Hello partes siguientes refinar Hola comunes [Mobile Engagement conceptos](mobile-engagement-concepts.md), para la plataforma Android Hola.

### <a name="session-and-activity"></a>`Session` y `Activity`
Si el usuario de hello permanece más de unos pocos segundos de inactividad entre dos *actividades*, a continuación, su secuencia de *actividades* se divide en dos distintos *sesiones*. Estos pocos segundos se denominan Hola "session timeout".

Un *actividad* suele estar asociado a una pantalla de la aplicación hello, que es hello toosay *actividad* se inicia cuando la pantalla de bienvenida se muestra y se detiene cuando se cierra la pantalla de bienvenida: se trata de hello caso en el que Hello Engagement SDK integrado utilizando hello `EngagementActivity` clases.

Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola. Esto permite toosplit una pantalla determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta pantalla (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta pantalla).

## <a name="reporting-activities"></a>Informes sobre actividades
> [!IMPORTANT]
> No es necesario tooreport actividades, como se describe en esta sección si usas hello `EngagementActivity` clase y sus variantes tal como se explica cómo Hola tooIntegrate interacción en documento Android.
> 
> 

### <a name="user-starts-a-new-activity"></a>El usuario inicia una nueva actividad
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Necesita toocall `startActivity()` cambia cada actividad de usuario de hello de tiempo. Hola primera llamada toothis función inicia una nueva sesión de usuario.

Hola mejor toocall lugar esta función es en cada actividad `onResume` devolución de llamada.

### <a name="user-ends-his-current-activity"></a>El usuario finaliza su actividad actual
            EngagementAgent.getInstance(this).endActivity();

Necesita toocall `endActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad. Este modo, informa Hola expirará Engagement SDK que usuario Hola está inactivo y que la sesión de usuario de hello necesario toobe una vez cerrado Hola tiempo de espera de sesión (si se llama a `startActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente se reanuda la sesión de hello).

Hola mejor toocall lugar esta función es en cada actividad `onPause` devolución de llamada.

## <a name="reporting-events"></a>Informes de eventos
### <a name="session-events"></a>Eventos de sesión
Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.

**Ejemplo sin datos adicionales:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Ejemplo con datos adicionales:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Eventos independientes
Eventos de toosession contrarias, pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.

**Ejemplo:**

Suponga que desea que se producen cuando se desencadena un difusión receptor de eventos de tooreport:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Informes de errores
### <a name="session-errors"></a>Errores de sesión
Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.

**Ejemplo:**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Errores independientes
Errores de toosession contrarias, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.

**Ejemplo:**

Hello en el ejemplo siguiente se muestra cómo tooreport un error cada vez que la memoria de Hola se queda corto de teléfono de Hola durante el proceso de la aplicación se ejecuta.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Informes de trabajos
### <a name="example"></a>Ejemplo
Suponga que desea tooreport Hola que dure el proceso de inicio de sesión:

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Informe de errores durante un trabajo
Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.

**Ejemplo:**

Suponga que desea tooreport un error durante la iniciar sesión proceso:

[...] inicio de sesión vacío público(Contexto contexto, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Notificación de eventos durante un trabajo
Pueden tooa relacionado ejecutando el trabajo en lugar de eventos relacionados con la sesión del usuario actual toohello.

**Ejemplo:**

Supongamos que tenemos una red social, y utilizamos un trabajo tooreport Hola tiempo total durante qué Hola usuario está conectado toohello server. usuario de Hello puede permanecer conectado en segundo plano incluso cuando está usando otra aplicación o al teléfono de hello está en espera, así que no hay ninguna sesión.

usuario de Hello puede recibir mensajes de sus amigos, se trata de un evento de trabajo.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Parámetros adicionales
Pueden ser datos arbitrarios tooevents adjunto, errores, las actividades y trabajos.

Estos datos se pueden estructurar y usan la clase Bundle de Android (en realidad, funcionan como los parámetros adicionales en los elementos Intent de Android). Tenga en cuenta que una clase Bundle puede contener matrices u otras instancias de Bundle.

> [!IMPORTANT]
> Si se coloca en los parámetros parcelable o serializables, asegúrese de que sus `toString()` método es tooreturn implementada una cadena legible para el usuario. Las clases serializables con campos no transitorios de tipo no serializable provocarán un bloqueo de Android cuando se llame a `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> No se admiten las matrices ralas en los parámetros adicionales, es decir, no se serializarán como matriz. Deberán convertirse en matrices estándar antes de usarlas en dichos parámetros.
> 
> 

### <a name="example"></a>Ejemplo
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Límites
#### <a name="keys"></a>simétricas
Cada clave de hello `Bundle` debe coincidir con la siguiente expresión regular de Hola:

`^[a-zA-Z][a-zA-Z_0-9]*`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Extras se limitan demasiado**1024** caracteres por llamada (una vez codificada en JSON mediante servicio de contratación de hello).

Hola ejemplo anterior, Hola JSON enviado toohello server es 58 caracteres:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Información de la aplicación de informes
Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de aplicación) con hello `sendAppInfo()` función.

Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.

Al igual que eventos adicionales, hello clase agrupación es tooabstract usa información de la aplicación, tenga en cuenta que las matrices o Sub-empaqueta se tratará como cadenas sin formato (con la serialización de JSON).

### <a name="example"></a>Ejemplo
Este es un sexo del usuario de toosend de ejemplo de código y la fecha de nacimiento:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>límites
#### <a name="keys"></a>simétricas
Cada clave de hello `Bundle` debe coincidir con la siguiente expresión regular de Hola:

`^[a-zA-Z][a-zA-Z_0-9]*`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Información de la aplicación se limitan demasiado**1024** caracteres por llamada (una vez codificada en JSON mediante servicio de contratación de hello).

Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:

            {"expiration":"2016-12-07","status":"premium"}
