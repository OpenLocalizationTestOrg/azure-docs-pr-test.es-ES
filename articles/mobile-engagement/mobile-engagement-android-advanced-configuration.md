---
title: "configuración de aaaAdvanced de Azure Mobile Engagement SDK de Android"
description: "Describe Hola incluidos Hola manifiesto Android con Azure Mobile Engagement Android SDK de opciones de configuración avanzada"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Configuración avanzada para el SDK de Android para Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Este procedimiento describe cómo tooconfigure distintas opciones de configuración para las aplicaciones de Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Requisitos de permiso
Algunas opciones requieren permisos específicos, todos ellos se enumeran aquí para referencia y en línea en la característica específica de Hola. Agregar estos toohello permisos AndroidManifest.xml del proyecto inmediatamente antes o después de hello `<application>` etiqueta.

código de Hello permiso debe toolook como Hola siguiente, donde se cumplimentan permiso adecuado de Hola de tabla de Hola que sigue.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Permiso | Cuándo se usa |
| --- | --- |
| INTERNET |Obligatorio. Para informes básicos |
| ACCESS_NETWORK_STATE |Obligatorio. Para informes básicos |
| RECEIVE_BOOT_COMPLETED |Necesario. tooshow el centro de notificaciones de hello tras el reinicio del dispositivo |
| WAKE_LOCK |Se recomienda su uso. Habilita la recopilación de datos cuando se usa la conexión WiFi o cuando la pantalla está apagada |
| VIBRATE |Opcional. Habilita la vibración cuando se reciben las notificaciones |
| DOWNLOAD_WITHOUT_NOTIFICATION |Opcional. Habilita la notificación de panorama general de Android |
| WRITE_EXTERNAL_STORAGE |Opcional. Habilita la notificación de panorama general de Android |
| ACCESS_COARSE_LOCATION |Opcional. Habilita los informes de ubicación en tiempo real |
| ACCESS_FINE_LOCATION |Opcional. Habilita los informes de ubicación basados en GPS |

A partir de Android M, [algunos permisos se administran en tiempo de ejecución](mobile-engagement-android-location-reporting.md#android-m-permissions).

Si ya usas ``ACCESS_FINE_LOCATION``, es necesario tooalso usar ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Opciones de configuración del manifiesto de Android
### <a name="crash-report"></a>Informe de bloqueos
informes de bloqueo de toodisable, agregue este código entre hello `<application>` y `</application>` etiquetas:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Umbral de ráfaga
De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real. Si los registros de informe de aplicaciones varían con frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (denominada "irrumpir modo"). toodo por lo tanto, agregue este código entre hello `<application>` y `</application>` etiquetas:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

El modo de ráfaga ligeramente aumenta la duración de la batería de hello pero tiene un impacto en el Monitor de interacción de hello: duración de las sesiones y los trabajos de todos los son toohello redondeado ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible). El umbral de ráfaga no debe ser superior a 30 000 (30 segundos).

### <a name="session-timeout"></a>Tiempo de espera de sesión
 Para terminar una actividad, al presionar hello **inicio** o **volver** clave, por teléfono de hello establecer inactivo o saltar a otra aplicación. De forma predeterminada, una sesión se finaliza diez segundos después del final de Hola de su última actividad. Esto evita una división de sesión cada vez que lo utiliza Hola cierre y devuelva toohello aplicación rápidamente, lo que puede ocurrir cuando el usuario de hello recoge una imagen, comprueba una notificación, etcetera. Puede que desee toomodify este parámetro. toodo por lo tanto, agregue este código entre hello `<application>` y `</application>` etiquetas:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Deshabilitación de los informes de registro
### <a name="using-a-method-call"></a>Mediante una llamada al método
Si desea enviar registros de toostop de interacción, puede llamar:

    EngagementAgent.getInstance(context).setEnabled(false);

Esta llamada es persistente: usa un archivo de preferencias compartido.

Si la interacción está activa cuando se llama a esta función, puede tardar un minuto para hello toostop de servicio. Sin embargo no inicie la próxima vez que inicia la aplicación hello servicio hello en hello todos los.

Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integración en su propia `PreferenceActivity`
En lugar de llamar a esta función, también puede integrar este valor directamente en su `PreferenceActivity` existente.

Puede configurar toouse de contratación sus preferencias de archivo (con el modo deseado de hello) de hello `AndroidManifest.xml` de archivos con `application meta-data`:

* Hola `engagement:agent:settings:name` clave es toodefine usado Hola nombre de archivo de preferencias compartidas hello.
* Hola `engagement:agent:settings:mode` clave es el modo de Hola de toodefine utilizado del archivo de preferencias compartidas Hola. Use Hola mismo modo que en su `PreferenceActivity`. modo de saludo se debe pasar como un número: Si usas una combinación de marcas de constantes en el código, compruebe el valor total de Hola.

Interacción siempre utiliza hello `engagement:key` booleano clave en el archivo de preferencias de Hola para administrar esta configuración.

Hola siguiendo el ejemplo de `AndroidManifest.xml` muestra Hola valores predeterminados:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

A continuación, puede agregar un `CheckBoxPreference` en el diseño de preferencias como Hola sigue uno:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
