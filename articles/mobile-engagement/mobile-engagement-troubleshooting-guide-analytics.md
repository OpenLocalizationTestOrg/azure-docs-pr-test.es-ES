---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - análisis"
description: "Solución de problemas de análisis, supervisión, segmentación y panel en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Guía de solución de problemas de análisis, supervisión, segmentación y panel
Hello siguientes son posibles problemas que pueden producirse con el modo en que Azure Mobile Engagement recopila información sobre los usuarios, dispositivos y aplicaciones.

## <a name="missingdelayed-information"></a>Información no encontrada o retrasada
### <a name="issue"></a>Problema
* La información se retrasa en aparecer en el análisis, la segmentación o el panel.
* Falta información en la supervisión.
* Falta información de análisis, de la segmentación o del panel.
* Alcanzar límites de segmentación.

### <a name="causes"></a>Causas
* Puede usar Hola API de análisis, API de Monitor, y API de segmentos toosee si los datos faltan desde la interfaz de usuario de hello es visible a través de hello API.
* Si hello Azure Mobile Engagement SDK no se integra correctamente en la aplicación no será capaz de toosee información Hola análisis, segmentación, supervisión o paneles.
* Los segmentos no se pueden cambiar una vez creados, solo se pueden "clonar" (copiar) o "destruir" (eliminar). Los segmentos solo pueden contener 10 criterios.
* Hola mejor manera tootest falta información de la supervisión es toosetup un dispositivo de prueba, desinstalar o volver a instalar la aplicación hello en dispositivo de prueba de Hola.
* La información se actualiza cada 24 horas para analizarla, segmentarla o para los paneles.
* Información de los nuevos segmentos no puede mostrarse hasta 24 horas después de que se creen incluso si el segmento de Hola se basa en la información anterior.
* Filtrado de los datos de análisis en la interfaz de usuario de hello le mostrará todos los ejemplos de este tipo, independientemente de la versión de hello de la aplicación (por ejemplo "se bloquea" filtrado por nombre mostrará desde las versiones 1 y 2 de la aplicación).
* Hello período de tiempo para el análisis se basa en hello fecha de la configuración de dispositivo de los usuarios de hello, por lo que un usuario cuyo teléfono tiene fecha Hola establecido incorrectamente podría aparecer en hello incorrecto período de tiempo.
* Inserta ningún servidor datos se registran cuando se usa el botón de hello demasiado "test", solo los datos se registran para las campañas de inserción real.

## <a name="cant-locate-items-in-ui"></a>No puede buscar los elementos de la interfaz de usuario
### <a name="issue"></a>Problema
* No se pueden crear segmentos basados en determinados criterios de etiqueta de información de la aplicación personalizada o integrada.
* No se puede encontrar determinados criterios de etiquetas de información de aplicación personalizada o integrada en análisis, supervisión o paneles.
* No se puede interpretar los datos de hello en análisis, supervisión, segmentación o paneles.

### <a name="causes"></a>Causas
* Algunas integradas en elementos e información de la aplicación etiquetas solo están disponibles como criterios de inserción, pero no puede agrega segmento tooa o visible desde el análisis, supervisión o panel. 
* En elementos e información de aplicación etiquetas que no se pueden agregan segmento tooa integrados, necesitará toosetup lista de destinatarios de criterios en cada hello tooperform de campaña la misma función que en función de un segmento de destino.
* Vea los menús contextuales de hello en secciones de análisis, supervisión, segmentación y paneles de Hola de hello interfaz de usuario de Azure Mobile Engagement para obtener más ayuda y cómo tooinformation.

## <a name="crash-troubleshooting"></a>Solución de problemas de bloqueos
### <a name="issue"></a>Problema
* Bloqueos de la aplicación que aparecen en el panel, supervisión o análisis.

### <a name="causes"></a>Causas
* tootroubleshoot aplicación se bloquea visto en el análisis, supervisión o panel realizar seguro toocheck Hola notas a los problemas conocidos con las versiones anteriores de hello SDK.
* toofurther solucionar problemas de aplicación realizan un evento desde un dispositivo de prueba con la aplicación se instale y buscar su ID de dispositivo en la sección de Hola "Monitor de – eventos" de la interfaz de usuario de Azure Mobile Engagement Hola los bloqueos. A continuación, realizar eventos Hola que esté ocasionando la toocrash de aplicación y buscar información adicional en hello "Monitor – bloquearse" sección de la interfaz de usuario de Azure Mobile Engagement Hola. 

