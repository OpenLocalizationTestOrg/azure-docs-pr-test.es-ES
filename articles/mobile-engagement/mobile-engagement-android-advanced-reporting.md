---
title: aaaAdvanced reporting opciones para Android SDK de Azure Mobile Engagement
description: "Describe cómo toodo informes toocapture análisis avanzados para Android SDK de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Informes avanzados con Engagement en Android
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Este tema describe los escenarios de informes adicionales en la aplicación Android. Puede aplicar estas aplicaciones de toohello opciones creado en hello [Introducción](mobile-engagement-android-get-started.md) tutorial.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

tutorial de Hola completó era deliberadamente sencillo y directo, pero existe son las opciones avanzadas que puede elegir.

## <a name="modifying-your-activity-classes"></a>Modificación de sus clases `Activity`
Hola [tutorial de introducción](mobile-engagement-android-get-started.md), todo lo que tenía toodo fue toomake su `*Activity` subclases heredan de hello correspondiente `Engagement*Activity` clases. Por ejemplo, si su actividad heredada amplía `ListActivity`, se ampliaría `EngagementListActivity` también.

> [!IMPORTANT]
> Cuando se usa `EngagementListActivity` o `EngagementExpandableListActivity`, asegúrese de que todas las llamadas demasiado`requestWindowFeature(...);` se realiza antes de la llamada de hello demasiado`super.onCreate(...);`, de lo contrario se produce un bloqueo.
> 
> 

Puede encontrar estas clases en hello `src` carpeta y puede copiarlos en el proyecto. clases de Hello también están en hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Método alternativo: llamar a `startActivity()` y `endActivity()` manualmente
Si no puede o no desea que toooverload su `Activity` clases, puede en su lugar, inicio y finalización de las actividades mediante una llamada a hello `EngagementAgent`de métodos directamente.

> [!IMPORTANT]
> Hola SDK de Android nunca llama hello `endActivity()` método, incluso cuando se cierra la aplicación hello (en Android, las aplicaciones nunca se cierran). Por lo tanto, es *alta* recomienda hello toocall `startActivity()` método Hola `onResume` devolución de llamada de *todos los* sus actividades y hello `endActivity()` método Hola `onPause()` devolución de llamada de *todos los* sus actividades. Se trata de toobe de manera única de hello seguro de que no se pierden las sesiones. Si una sesión se ha filtrado, Hola servicio interacción nunca se desconecta de backend de interacción de hello (ya que servicio Hola permanece conectado mientras está pendiente una sesión).
> 
> 

Aquí tiene un ejemplo:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

En este ejemplo es similar toohello `EngagementActivity` clase y sus variantes, cuyo código fuente se proporciona en hello `src` carpeta.

## <a name="using-applicationoncreate"></a>Uso de Application.onCreate()
Cualquier código que se coloque en `Application.onCreate()` y en otra aplicación, las devoluciones de llamada se ejecuta para los procesos de todas las de su aplicación, incluido el servicio de contratación de Hola. Puede tener efectos secundarios no deseados, como las asignaciones de memoria innecesario y subprocesos en el proceso de contratación de hello, o duplicado difusión receptores o servicios.

Si invalida `Application.onCreate()`, se recomienda agregar Hola siguiente fragmento de código al principio de Hola de su `Application.onCreate()` función:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Puede hacer lo mismo para Hola `Application.onTerminate()`, `Application.onLowMemory()`, y `Application.onConfigurationChanged(...)`.

También puede extender `EngagementApplication` en lugar de extender `Application`: Hola de devolución de llamada `Application.onCreate()` Hola comprobación del proceso y llamadas `Application.onApplicationProcessCreate()` solo si proceso actual de hello es no Hola uno Hola interacción servicio de hospedaje, hello mismas reglas se aplican para Hola otras devoluciones de llamada.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Etiquetas en el archivo AndroidManifest.xml Hola
En la etiqueta de servicio de hello en el archivo AndroidManifest.xml hello, Hola `android:label` atributo permite toochoose Hola nombre de servicio de contratación de hello tal y como aparece tooend a los usuarios en la pantalla de bienvenida "Ejecutar servicios" de su teléfono. Se recomienda establecer este atributo demasiado`"<Your application name>Service"` (por ejemplo, `"AcmeFunGameService"`).

Hola especificando `android:process` atributo garantiza que Hola se ejecuta en su propio proceso (ejecutando interacción en el mismo proceso cuando la aplicación realiza el subproceso de interfaz de usuario/main potencialmente menos capacidad de respuesta de Hola) en el servicio de contratación.

## <a name="building-with-proguard"></a>Compilación con ProGuard
Si compila el paquete de aplicación con ProGuard, deberá tookeep algunas clases. Puede usar Hola siguiente fragmento de código de configuración:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
