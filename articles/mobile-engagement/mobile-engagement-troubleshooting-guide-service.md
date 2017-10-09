---
title: aaaAzure Mobile Engagement Troubleshooting Guide - servicio
description: "Guías de solución de problemas de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Guía de solución de problemas de servicio
los siguientes Hola son posibles problemas que pueden producirse con cómo se ejecuta Azure Mobile Engagement.

## <a name="service-outages"></a>Interrupciones del servicio
### <a name="issue"></a>Problema
* Problemas que aparecen toobe causado por interrupciones de servicio de Azure Mobile Engagement.

### <a name="causes"></a>Causas
* Problemas que aparecen toobe causado por interrupciones de servicio de Azure Mobile Engagement pueden deberse a diversos problemas:
  * Problemas aislados que originalmente aparecen tooall sistémica de Azure Mobile Engagement
  * Problemas conocidos causados por interrupciones de los servidores (no siempre se muestran en el estado del servidor):
  * Programación retrasos, Targeting errores, problemas de actualización de distintivo, stop estadísticas recopilando, deja de inserción funcionar, dejan de funcionar, nuevas aplicaciones o los usuarios de la API no se puede crear, errores de DNS y los errores de tiempo de espera en hello IU, API o aplicaciones en un dispositivo.
  * Interrupciones de dependencia en la nube [Estado del servicio de Azure](http://status.azure.com/)
  * Interrupciones de dependencia de los servicios de notificación de inserción (PNS)
  * Interrupciones de la tienda de aplicaciones

1) tootest toosee si el problema de hello es sistémico puede probar Hola la misma función de otra

* Aplicación integrada de Azure Mobile Engagement
* Dispositivo de prueba
* Versión del sistema operativo del dispositivo de prueba
* Campaña
* Cuenta de usuario administrador
* Explorador (Internet Explorer, Firefox, Chrome, etc.)
* Equipo

2) tootest si Hola solo problema Hola Hola o interfaz de usuario de la API:

* Probar Hola misma función de ambos Hola interfaz de usuario de Azure Mobile Engagement y Hola la API de Azure Mobile Engagement.

3) tootest si el problema de hello está relacionado con la red de telefonía móvil:

* Probar al toohello conectado a Internet a través de Wi-Fi y mientras se está conectado a través de la red de telefonía móvil 3G.
* Confirme que el firewall no bloquee cualquiera de las direcciones IP hello Azure Mobile Engagement o puertos.

4) tootest si el problema de hello está relacionado con el dispositivo:

* Comprueba si el dispositivo es capaz de tooconnect tooAzure Mobile Engagement con otra aplicación de Azure Mobile Engagement integrado.
* Compruebe que puede generar eventos, los trabajos y bloqueos desde el teléfono que se pueden ver en la interfaz de usuario de Azure Mobile Engagement Hola. 
* Probar si puede enviar notificaciones de inserción de dispositivo de tooyour de interfaz de usuario de Azure Mobile Engagement Hola basándose en su identificador de dispositivo. 

5) tootest si el problema de hello está relacionado con la aplicación:

* Instale y pruebe la aplicación desde un emulador en lugar de hacerlo desde un dispositivo físico:

6) tootest si el problema de hello es con un sistema operativo actualiza tooend usuario dispositivos, que requieren un tooresolve de actualización de SDK:

* Probar la aplicación en distintos dispositivos con distintas versiones de SO Hola.
* Confirme que está utilizando la versión más reciente de Hola de hello SDK.

## <a name="connectivity-and-incorrect-information-issues"></a>Problemas de conectividad e información incorrecta
### <a name="issue"></a>Problema
* Problemas para iniciar sesión en Hola interfaz de usuario de Azure Mobile Engagement.
* Errores de conexión con hello Azure Mobile Engagement API.
* Problemas al cargar las etiquetas de información de aplicación a través de hello API de dispositivo.
* Problemas de descarga de registros o datos exportados desde Azure Mobile Engagement.
* Información incorrecta que se muestra en la interfaz de usuario de Azure Mobile Engagement Hola.
* Información incorrecta que se muestra en los registros de Azure Mobile Engagement.

### <a name="causes"></a>Causas
* Confirme que su cuenta de usuario tiene la tarea de hello de tooperform de permisos suficientes.
* Confirme que error hello no está aislado tooone equipo o la red local.
* Confirme que ese servicio de Azure Mobile Engagement hello no tiene ningún las interrupciones registradas.
* Confirme que los archivos de la etiqueta de información de la aplicación siguen todas estas reglas:
  * Use solo Hola juego de caracteres UTF8 (no se admite el juego de caracteres ANSI de hello).
  * Use una coma "," como carácter de separador de hello (puede abrir un carácter de separador de servicio solicitud toorequest toochange Hola .csv desde una coma "," carácter tooanother como un punto y coma ";").
  * Use minúsculas para los valores booleanos "true" y "false".
  * Usar un archivo que es inferior al tamaño de archivo máximo de Hola de 35MB.

