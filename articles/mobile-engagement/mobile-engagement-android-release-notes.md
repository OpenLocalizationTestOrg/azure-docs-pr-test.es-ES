---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Notas de la versión

## <a name="431-07172017"></a>4.3.1 (17/07/2017)
* Se ha corregido un bloqueo que rara vez puede suceder cuando se llama a `EngagementAgentUtils.isInDedicatedEngagementProcess`, que también usan hello `EngagementApplication` clase.

## <a name="430-06272017"></a>4.3.0 (27/06/2017)
* Android admiten 8 (versiones anteriores de hello SDK no funcionarán en Android 8).
* Desaparece la dependencia de la biblioteca de soporte.
* Se quita la clase `EngagementFragmentActivity`.
* Vencimiento demasiado[límites de la ejecución de fondo](https://developer.android.com/preview/features/background.html) en 8 Android, registros en segundo plano se retrasa hasta que el usuario de hello interactúa con el dispositivo de hello, esto tendrá un impacto en la campaña de inserción **entregados** y **Notificación del sistema mostrada** estadísticas que se retrasa si se encontraba inactivo el dispositivo hello (Hola notificación seguirán mostrándose, se anillo y Vibrar en tiempo real sin problemas).
* Vencimiento demasiado[límites de ubicación de fondo](https://developer.android.com/preview/features/background-location-limits.html), ubicación de tiempo real de hello en segundo plano no se actualizará con frecuencia en 8 Android.

## <a name="424-03302017"></a>4.2.4 (30/03/2017)
* Corregir la notificación en la aplicación Hola colores de texto en 7 Android toobe igual que en versiones anteriores de Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* No se producirán más bloqueos de WiFi.
* Se ha corregido un interbloqueo al llamar a getDeviceId antes de init (error de la versión 4.2.0).

## <a name="422-05172016"></a>4.2.2 (17/05/2016)
* Mejoras de estabilidad.

## <a name="421-05102016"></a>4.2.1 (10/05/2016)
* Seguridad: deshabilite el acceso a archivos locales de la vista web.
* Seguridad: quite la clase `EngagementPreferenceActivity` que extiende la clase `PreferenceActivity` no segura y obsoleta.
* Seguridad: alcance actividades ahora están documentados toouse `exported="false"`, esta marca también puede usarse en versiones anteriores del SDK.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Hola SDK ahora con licencia bajo MIT.
* Permite especificar un identificador de dispositivo personalizado en el tiempo de inicialización del SDK.

## <a name="415-02012016"></a>4.1.5 (02/01/2016)
* Mejoras de estabilidad.

## <a name="414-01262016"></a>4.1.4 (01/26/2016)
* Mejoras de estabilidad.

## <a name="413-1292015"></a>4.1.3 (9/12/2015)
* Mejoras de estabilidad.

## <a name="412-11252015"></a>4.1.2 (25/11/2015)
* Mejoras de estabilidad.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* Mejoras de estabilidad.

## <a name="410-08252015"></a>4.1.0 (08/25/2015)
* Controle el nuevo modelo de permiso para Android M.
* Ahora puede configurar las características de ubicación en tiempo de ejecución en lugar de usar `AndroidManifest.xml`.
* Corrija un error de permiso: si usa `ACCESS_FINE_LOCATION`, ya no necesita `ACCESS_COARSE_LOCATION`.
* Mejoras de estabilidad.

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* Protocolo interno cambia toomake análisis y más confiable de inserción.
* Inserción nativa (GCM/ADM) ahora también se utiliza para las notificaciones en aplicación por lo que debe configurar credenciales de inserción nativa de Hola para cualquier tipo de campaña de inserción.
* Corrección de la notificación con imagen grande: se mostraban solo 10 s después de insertarse.
* Corregir un error en la vista web: al hacer clic en un vínculo también estaba ejecutando la URL de acción predeterminada de Hola.
* Se ha corregido un bloqueo excepcional relacionados con la administración de almacenamiento de toolocal.
* Corrección de la administración dinámica de cadenas de configuración.
* Actualización del CLUF.

## <a name="300-02172015"></a>3.0.0 (02/17/2015)
* Versión inicial de Azure Mobile Engagement
* La configuración de appID se reemplaza por una configuración de cadena de conexión.
* Quitar toosend de API y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.
* Quitar toosend de API y recibir mensajes entre los dispositivos.
* Mejoras de seguridad.
* Seguimiento de SmartAd y Google Play eliminados.

