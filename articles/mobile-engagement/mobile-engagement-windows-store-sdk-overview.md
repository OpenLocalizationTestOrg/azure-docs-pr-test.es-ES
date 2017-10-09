---
title: "aaaAzure integración Universal de SDK de Mobile Engagement Windows | Documentos de Microsoft"
description: "Integración del SDK de Windows Universal para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Integración del SDK de Windows Universal para Azure Mobile Engagement
Este documento describe todos los Hola integración y configuración de opciones disponibles para hello Azure Mobile Engagement Windows Universal SDK.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, primero debe completar la [Introducción a Azure Mobile Engagement para aplicaciones Android](mobile-engagement-windows-store-dotnet-get-started.md), un tutorial de 15 minutos.

## <a name="advanced-features"></a>Características avanzadas
### <a name="reporting-features"></a>Características de informes
Puede agregar estas características:

1. [Opciones de informes avanzados](mobile-engagement-windows-store-advanced-reporting.md)
2. [Opciones de configuración avanzada](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Notificaciones
[¿Cómo toointegrate alcance (notificaciones) en la aplicación Universal de Windows](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Implementación del plan de etiquetas:
[¿Cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Notas de la versión
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Mejoras de estabilidad.

Para las versiones anteriores, vea hello [completar notas de la versión](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Si se perdió varias versiones del SDK de hello, habrá toofollow varios procedimientos. Vea Hola completa [actualizar procedimientos](mobile-engagement-windows-store-upgrade-procedure.md). Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.

### <a name="from-330-too340"></a>Desde 3.3.0 too3.4.0
#### <a name="test-logs"></a>Registros de prueba
Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado. toocustomize, actualizar la propiedad de hello `EngagementAgent.Instance.TestLogEnabled` tooone de valores de hello disponibles de hello `EngagementTestLogLevel` enumeración, por ejemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Recursos
se ha mejorado la superposición de cobertura de Hola. Forma parte de recursos del paquete de NuGet de SDK de Hola.

Durante la actualización toohello nueva versión de hello SDK, puede elegir que si desea que tookeep los archivos existentes de hello superposición de carpeta de los recursos:

* Si superposición anterior Hola funciona para usted, o va a integrar hello `WebView` elementos manualmente, a continuación, puede decidir salir de los archivos tookeep, seguirá funcionando.
* tooupdate toohello nueva superposición, Hola de reemplazar todo `overlay` carpeta de sus recursos con hello nueva del paquete SDK de hello (aplicaciones UWP: después de la actualización de hello, puede obtener nueva carpeta de superposición Hola desde % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Utilizando la superposición de hello nueva sobrescribe todas las personalizaciones realizadas en la versión anterior de Hola.
> 
> 

### <a name="upgrade-from-older-versions"></a>Actualizar de versiones anteriores
Consulte [Procedimientos de actualización](mobile-engagement-windows-store-upgrade-procedure.md)

