---
title: "aaaHow tooUse Hola API de interacción de Windows Phone Silverlight"
description: "¿Cómo tooUse Hola API de interacción de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>¿Cómo tooUse Hola API de interacción de Windows Phone Silverlight
Este documento es un complemento toohello [cómo toointegrate Mobile Engagement en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md). Proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.

Si sólo desea interacción tooreport sesiones, actividades, bloqueos e información técnica de la aplicación, hello más sencillo cierto es toomake todos los su `PhoneApplicationPage` subclases heredan de hello `EngagementPage` clase.

Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementPage` clases, deberá toouse Hola API de contratación.

Hello interacción API proporcionada por hello `EngagementAgent` clase. Puede tener acceso a los métodos de toothose a través de `EngagementAgent.Instance`.

Incluso si no se ha inicializado el módulo de agente de hello, cada API toohello de llamada se pospone y se ejecutará de nuevo cuando el agente Hola está disponible.

## <a name="engagement-concepts"></a>Conceptos de Engagement
Hola siguientes piezas refinar Hola Mobile Engagement conceptos para la plataforma de Windows Phone Hola.

### <a name="session-and-activity"></a>`Session` y `Activity`
Un *actividad* suele estar asociado a una página de aplicación hello, que es hello toosay *actividad* se inicia cuando la página de Hola se muestra y se detiene cuando se cierra la página de Hola: se trata de los casos de hello cuando hello Engagement SDK se integra mediante hello `EngagementPage` clase.

Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola. Esto permite toosplit una página determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta página (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta página).

## <a name="reporting-activities"></a>Informes sobre actividades
### <a name="user-starts-a-new-activity"></a>El usuario inicia una nueva actividad
#### <a name="reference"></a>Referencia
            void StartActivity(string name, Dictionary<object, object> extras = null)

Necesita toocall `StartActivity()` cambia cada actividad de usuario de hello de tiempo. Hola primera llamada toothis función inicia una nueva sesión de usuario.

> [!IMPORTANT]
> Hola SDK automáticamente llame al método EndActivity de hello cuando se cierra la aplicación hello. Por lo tanto, se recomienda encarecidamente método de toocall hello StartActivity cada vez que ha finalizado la actividad de hello del cambio de usuario de Hola y llamada tooNEVER Hola método EndActivity, desde una llamada a este método obliga a toobe de la sesión actual de Hola.
> 
> 

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>El usuario finaliza su actividad actual
#### <a name="reference"></a>Referencia
            void EndActivity()

Necesita toocall `EndActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad. Este modo, informa Hola expirará Engagement SDK que usuario Hola está inactivo y que la sesión de usuario de hello necesario toobe una vez cerrado Hola tiempo de espera de sesión (si se llama a `StartActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente continúa sesión hello).

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Informes de trabajos
### <a name="start-a-job"></a>Iniciar un trabajo
#### <a name="reference"></a>Referencia
            void StartJob(string name, Dictionary<object, object> extras = null)

Puede utilizar tareas de hello trabajo tootrack ciertos durante un período de tiempo.

#### <a name="example"></a>Ejemplo
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Finalizar un trabajo
#### <a name="reference"></a>Referencia
            void EndJob(string name)

Tan pronto como se ha terminado una tarea que realiza el seguimiento de un trabajo, se debería llamar a hello EndJob método para este trabajo, proporcionando el nombre del trabajo de Hola.

#### <a name="example"></a>Ejemplo
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Informes de eventos
Hay tres tipos de eventos:

* Eventos independientes
* Eventos de sesión
* Eventos de trabajo

### <a name="standalone-events"></a>Eventos independientes
#### <a name="reference"></a>Referencia
            void SendEvent(string name, Dictionary<object, object> extras = null)

Pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Eventos de sesión
#### <a name="reference"></a>Referencia
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.

#### <a name="example"></a>Ejemplo
**Sin datos:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Con datos:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Eventos de trabajo
#### <a name="reference"></a>Referencia
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Eventos de trabajo son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante un trabajo.

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Informes de errores
Hay tres tipos de errores:

* Errores independientes
* Errores de sesión
* Errores de trabajo

### <a name="standalone-errors"></a>Errores independientes
#### <a name="reference"></a>Referencia
            void SendError(string name, Dictionary<object, object> extras = null)

Errores de toosession contrarias, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Errores de sesión
#### <a name="reference"></a>Referencia
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Errores de trabajo
#### <a name="reference"></a>Referencia
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.

#### <a name="example"></a>Ejemplo
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Informes de bloqueos
agente de Hello proporciona dos toodeal métodos con los bloqueos.

### <a name="send-an-exception"></a>Enviar una excepción
#### <a name="reference"></a>Referencia
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Ejemplo
Puede enviar una excepción en cualquier momento al llamar a:

            EngagementAgent.Instance.SendCrash(aCatchedException);

También puede utilizar una sesión de interacción de parámetro opcional tooterminate hello en hello mismo tiempo que el envío de bloqueo de Hola. por lo tanto, llame la toodo:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Si lo hace, trabajos y sesión Hola se cerrará inmediatamente después de enviar el bloqueo de Hola.

### <a name="send-an-unhandled-exception"></a>Enviar una excepción no controlada
#### <a name="reference"></a>Referencia
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Interacción también proporciona un excepciones de toosend no controlada por el método. Esto es especialmente útil cuando se usa dentro del controlador de eventos de hello silverlight UnhandledException.

Este método le **siempre** finalizar sesión de interacción de Hola y trabajos tras la llamada.

#### <a name="example"></a>Ejemplo
Puede usar tooimplement su propio controlador UnhandledException (especialmente si ha deshabilitado la característica de interacción de informes de bloqueo automática hello). Por ejemplo, en hello `Application_UnhandledException` método de hello `App.xaml.cs` archivo:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>Referencia
            void OnActivated(ActivatedEventArgs e)

Al usuario Hola se desplaza hacia delante, fuera de una aplicación, después de que se genera el evento de hello desactivado, sistema operativo de hello tratará de aplicación de hello tooput en estado inactivo. A continuación, la aplicación hello es extinción. En este proceso se termina una aplicación, pero se conservan algunos datos sobre el estado de Hola de hello páginas de aplicación y Hola individuales dentro de la aplicación hello.

Tiene tooinsert `EngagementAgent.Instance.OnActivated(e)` en hello `Application_Activated` método de Hola de tooreset de archivo hello App.xaml.cs interacción agente cuando aplicación hello se ha desechado.

### <a name="example"></a>Ejemplo
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>Identificador de dispositivo
            String GetDeviceId()

Puede obtener Id. de dispositivo de interacción de hello mediante una llamada a este método.

## <a name="extras-parameters"></a>Parámetros adicionales
Evento tooan adjunto, un error, una actividad o un trabajo, pueden ser datos arbitrarios. Estos datos se pueden estructurar mediante un diccionario. Las claves y los valores pueden ser de cualquier tipo.

Por lo que si desea tooinsert su propio tipo de extras tener tooadd un contrato de datos para este tipo, se serializan datos adicionales.

### <a name="example"></a>Ejemplo
Creamos una nueva clase "Person".

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

A continuación, agregaremos un `Person` tooan de instancia adicional.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Si coloca otros tipos de objetos, asegúrese de que su método ToString() es tooreturn implementada una cadena legible.
> 
> 

### <a name="limits"></a>límites
#### <a name="keys"></a>simétricas
Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Extras se limitan demasiado**1024** caracteres por llamada.

## <a name="reporting-application-information"></a>Información de la aplicación de informes
### <a name="reference"></a>Referencia
            void SendAppInfo(Dictionary<object, object> appInfos)

Puede crear informes manualmente información (o cualquier otra información específica de aplicación) con hello SendAppInfo() función de seguimiento.

Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado. Como eventos adicionales, utilice un diccionario\<(objeto), objeto\> tooattach informaciones.

### <a name="example"></a>Ejemplo
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Límites
#### <a name="keys"></a>simétricas
Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).

#### <a name="size"></a>Tamaño
Información de la aplicación se limitan demasiado**1024** caracteres por llamada.

Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>Registro
### <a name="enable-logging"></a>Habilitación del registro
Hola SDK puede ser tooproduce configurado los registros de pruebas en la consola de hello IDE.
Estos registros no están activados de forma predeterminada. toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
