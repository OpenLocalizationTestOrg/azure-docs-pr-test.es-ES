---
title: "aaaHow tooadd un entorno de centro de eventos eventos origen tooyour visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "Este tutorial trata cómo tooadd un evento que es origen conectado tooan concentrador de eventos tooyour visión de la serie de tiempo entorno"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>¿Cómo tooadd un origen de eventos de concentrador de eventos

Este tutorial trata cómo toouse Hola tooadd de portal de Azure a un origen de eventos que se lee de un entorno de centro de eventos tooyour visión de la serie de tiempo.

## <a name="prerequisites"></a>Requisitos previos

Ha creado un centro de eventos y se escribe tooit de eventos. Para más información sobre centros de eventos, vea <https://azure.microsoft.com/services/event-hubs/>.

> [Grupos de consumidores] Cada origen de eventos de información de la serie de tiempo debe toohave su propio grupo de consumidores dedicado que no se comparte con otros consumidores. Si varios lectores consumen eventos de Hola mismo grupo de consumidores, todos los lectores son errores de toosee probable. Tenga en cuenta que también hay un límite de 20 grupos de consumidores por Centro de eventos. Para obtener más información, vea hello [Guía de programación de los centros de eventos](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Selección de un opción de importación

configuración de Hola Hola origen de eventos puede escribirse manualmente o se puede seleccionar un concentrador de eventos Hola los centros de eventos que están disponible tooyou.
Hola **opción importar** selector, elija una de las siguientes opciones de hello:

* Proporcionar configuración del centro de eventos de forma manual
* Usar el centro de eventos desde suscripciones disponibles

### <a name="select-an-available-event-hub"></a>Seleccionar un centro de eventos disponible

Hello tabla siguiente explica cada opción en la pestaña del nuevo origen de eventos de hello con su descripción cuando se selecciona un concentrador de eventos disponibles como un origen de eventos:

| Nombre de propiedad | Description |
| --- | --- |
| Nombre de origen de eventos | nombre de Hola de su origen de eventos. Este nombre debe ser único dentro del entorno de Time Series Insights.
| Origen | Elija **concentrador de eventos** toocreate un origen de eventos de concentrador de eventos.
| Id. de suscripción | Seleccione la suscripción de hello en el que se creó este concentrador de eventos.
| Espacio de nombres de Service bus | Seleccione el espacio de nombres de Bus de servicio de Hola que contiene Hola concentrador de eventos.
| Nombre del centro de eventos | Seleccione el nombre de Hola de hello concentrador de eventos.
| Nombre de la directiva del centro de eventos | Seleccione la directiva de acceso de hello compartido, que se puede crear en la pestaña Configurar centro de eventos de Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. Hola las directivas de acceso para el origen del evento compartido *debe* tienen **leer** permisos.
| Grupo de consumidores de centro de eventos | Hola eventos de grupo de consumidores tooread de hello concentrador de eventos. Es muy recomendable toouse un grupo de consumidores dedicado para el origen del evento.

### <a name="provide-event-hub-settings-manually"></a>Proporcionar configuración del centro de eventos de forma manual

Hello tabla siguiente explica cada propiedad en la pestaña del nuevo origen de eventos de hello con su descripción al especificar la configuración manualmente:

| Nombre de propiedad | Description |
| --- | --- |
| Nombre de origen de eventos | nombre de Hola de su origen de eventos. Este nombre debe ser único dentro del entorno de Time Series Insights.
| Origen | Elija **concentrador de eventos** toocreate un origen de eventos de concentrador de eventos.
| Id. de suscripción | suscripción de Hello en el que se creó este concentrador de eventos.
| Grupos de recursos | suscripción de Hello en el que se creó este concentrador de eventos.
| Espacio de nombres de Service bus | Un espacio de nombres del bus de servicio es un contenedor para un conjunto de entidades de mensajería. Al crear un nuevo centro de eventos, también se crea un espacio de nombres del Bus de servicio.
| Nombre del centro de eventos | nombre de Hola de su centro de eventos. Cuando creó el centro de eventos, también le asignó un nombre específico.
| Nombre de la directiva del centro de eventos | Hola directiva de acceso compartido, que se puede crear en la pestaña Configurar centro de eventos de Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. Hola las directivas de acceso para el origen del evento compartido *debe* tienen **leer** permisos.
| Clave de la directiva de centro de eventos | clave de acceso compartido de Hello usa el espacio de nombres de tooauthenticate acceso toohello Bus de servicio. Escriba Hola clave primaria o secundaria aquí.
| Grupo de consumidores de centro de eventos | Hola eventos de grupo de consumidores tooread de hello concentrador de eventos. Es muy recomendable toouse un grupo de consumidores dedicado para el origen del evento.

## <a name="next-steps"></a>Pasos siguientes

1. Agregar un entorno de tooyour de directiva de acceso de datos [datos definir directivas de acceso](time-series-insights-data-access.md)
1. Obtener acceso a su entorno en hello [Portal de visión de Series de tiempo](https://insights.timeseries.azure.com)
