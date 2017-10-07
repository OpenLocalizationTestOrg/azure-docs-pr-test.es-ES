---
title: "aaaAzure notas de la versión de SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Notas de la versión del SDK de iOS de Azure Mobile Engagement

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Se han corregido las notificaciones borradas en el fondo.
* Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.
* Se ha corregido una fuga de memoria en los sondeos de cobertura.
* Se ha eliminado el soporte técnico para iOS 6.X. A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 7.

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* Entrega de registros en segundo plano mejorada

## <a name="400-09122016"></a>4.0.0 (09/12/2016)
* Notificación fija no ejecutada en dispositivos iOS 10.
* XCode 7 en desuso.

## <a name="324-06302016"></a>3.2.4 (30/06/2016)
* Agregación fija entre registros técnicos y otros registros.

## <a name="323-06072016"></a>3.2.3 (06/07/2016)
* Error de hello fijo en comentarios de entrega no se notifican cuando la aplicación se encuentra en segundo plano de Hola.
* Hola optimizado envío de registros técnicos.

## <a name="322-04072016"></a>3.2.2 (04/07/2016)
* Ha corregido el error en la cancelación de la solicitud HTTP que conduce a veces toocrash.

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* Retraso de hello fijo cuando se desencadena una nueva instancia de la aplicación mediante una notificación con vínculos profundos

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Habilitado Bitcode en hello SDK toomake funciona con **Xcode 7**.
* Los errores corregidos relacionados con las notificaciones de la aplicación tooin.
* Realiza las notificaciones de la aplicación hello más confiable en el caso de batería baja y otros escenarios de este tipo.
* Se quitaron registros de la consola adicionales generados por la biblioteca de terceros.

## <a name="310-08262015"></a>3.1.0 (08/26/2015)
* Corrija los errores de compatibilidad de iOS 9 con una biblioteca de terceros. Generaban bloqueos al enviar resultados de sondeo, información de la aplicación o datos adicionales.

## <a name="300-06192015"></a>3.0.0 (19/06/2015)
* Mobile Engagement usa notificaciones push silenciosas.
* Soporte de iOS 4.X eliminado. A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 6.

## <a name="220-05212015"></a>2.2.0 (05/21/2015)
* Id. de dispositivo de Hello Mobile Engagement para dispositivos < iOS 6 se basa ahora en un GUID generado durante la instalación.

## <a name="210-04242015"></a>2.1.0 (24/04/2015)
* Agregada compatibilidad con Swift.
* Al hacer clic en una notificación, acción de hello que dirección URL es ahora ejecuta derecha cuando se abre la aplicación hello.
* Se ha agregado el archivo de encabezado que faltaba en el paquete del SDK.
* Se corrigió un problema cuando se deshabilitó el indicador de bloqueo de Mobile Engagement Hola.

## <a name="200-02172015"></a>2.0.0 (02/17/2015)
* Versión inicial de Azure Mobile Engagement
* La configuración de appId o sdkKey se sustituye por una configuración de la cadena de conexión.
* Quitar toosend de API y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.
* Quitar toosend de API y recibir mensajes entre los dispositivos.
* Mejoras de seguridad.
* Se ha eliminado el seguimiento de SmartAd.
