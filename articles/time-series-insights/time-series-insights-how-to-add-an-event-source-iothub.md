---
title: "aaaHow tooadd un entorno de centro de IoT eventos origen tooyour visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "Este tutorial trata cómo tooadd un evento de origen que es conectado tooan entorno de centro de IoT tooyour visión de la serie de tiempo"
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>¿Cómo tooadd un origen de eventos de centro de IoT

Este tutorial trata cómo toouse Hola tooadd de portal de Azure a un origen de eventos que se lee de un entorno de centro de IoT tooyour visión de la serie de tiempo.

## <a name="prerequisites"></a>Requisitos previos

Ha creado un centro de IoT y está escribiendo tooit de eventos. Para más información sobre IoT Hubs, vea <https://azure.microsoft.com/services/iot-hub/>

> [Grupos de consumidores] Cada origen de eventos de información de la serie de tiempo debe toohave su propio grupo de consumidores dedicado que no se comparte con otros consumidores. Si varios lectores consumen eventos de Hola mismo grupo de consumidores, todos los lectores son errores de toosee probable. Para obtener más información, vea hello [Guía del desarrollador de centro de IoT](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Selección de un opción de importación

configuración de Hola Hola origen de eventos puede escribirse manualmente o se puede seleccionar un centro de IoT desde los centros de IoT de Hola que están disponible tooyou.
Hola **opción importar** selector, elija una de las siguientes opciones de hello:

* Proporcionar configuración de IoT Hub de forma manual
* Usar IoT Hub desde suscripciones disponibles

### <a name="select-an-available-iot-hub"></a>Seleccionar un IoT Hub disponible

Hello tabla siguiente explica cada opción en la pestaña del nuevo origen de eventos de hello con su descripción al seleccionar un centro de IoT disponible como un origen de eventos:

| Nombre de propiedad | Description |
| --- | --- |
| Nombre de origen de eventos | nombre de Hola de su origen de eventos. Este nombre debe ser único dentro del entorno de Time Series Insights.
| Origen | Elija **centro de IoT** toocreate un origen de eventos de centro de IoT.
| Id. de suscripción | Seleccione la suscripción de hello en el que se creó este centro de IoT.
| Nombre de IoT Hub | Seleccione el nombre de Hola de hello centro de IoT.
| Nombre de la directiva de IoT Hub | Seleccione la directiva de acceso de hello compartido, que se encuentra en la ficha de configuración del centro de IoT Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. Hola las directivas de acceso para el origen del evento compartido *debe* tienen **servicio conectar** permisos.
| Grupo de consumidores de IoT Hub | Hola eventos de grupo de consumidores tooread de hello centro de IoT. Es muy recomendable toouse un grupo de consumidores dedicado para el origen del evento.

### <a name="provide-iot-hub-settings-manually"></a>Proporcionar configuración de IoT Hub de forma manual

Hello tabla siguiente explica cada propiedad en la pestaña del nuevo origen de eventos de hello con su descripción al especificar la configuración manualmente:

| Nombre de propiedad | Description |
| --- | --- |
| Nombre de origen de eventos | nombre de Hola de su origen de eventos. Este nombre debe ser único dentro del entorno de Time Series Insights.
| Origen | Elija **centro de IoT** toocreate un origen de eventos de centro de IoT.
| Id. de suscripción | suscripción de Hello en el que se creó este centro de IoT.
| Grupos de recursos | suscripción de Hello en el que se creó este centro de IoT.
| Nombre de IoT Hub | nombre de Hola de su centro de IoT. Cuando creó IoT Hub, también le asignó un nombre específico.
| Nombre de la directiva de IoT Hub | Directiva de acceso de Hello compartido, que se puede crear en la pestaña de configuración del centro de IoT Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. Hola las directivas de acceso para el origen del evento compartido *debe* tienen **servicio conectar** permisos.
| Clave de la directiva de IoT Hub | clave de acceso compartido de Hello usa el espacio de nombres de tooauthenticate acceso toohello Bus de servicio. Escriba Hola clave primaria o secundaria aquí.
| Grupo de consumidores de IoT Hub | Hola eventos de grupo de consumidores tooread de hello centro de IoT. Es muy recomendable toouse un grupo de consumidores dedicado para el origen del evento.

## <a name="next-steps"></a>Pasos siguientes

1. Agregar un entorno de tooyour de directiva de acceso de datos [datos definir directivas de acceso](time-series-insights-data-access.md)
1. Obtener acceso a su entorno en hello [Portal de visión de Series de tiempo](https://insights.timeseries.azure.com)
