---
title: "filtros de conexión de IP del centro de IoT aaaAzure | Documentos de Microsoft"
description: "Cómo las direcciones IP toouse filtrado de conexiones de tooblock de IP específica para tooyour centro de IoT de Azure. Puede bloquear conexiones de direcciones IP concretas o de intervalos."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Uso de filtros IP

La seguridad es un aspecto importante de cualquier solución de IoT basada en Azure IoT Hub. En ciertas ocasiones necesitará tooexplicitly especificar direcciones IP de Hola desde el que pueden conectar dispositivos como parte de la configuración de seguridad. Hola _filtro IP_ característica permite tooconfigure reglas para rechazar o aceptar tráfico de direcciones IPv4 específicas.

## <a name="when-toouse"></a>Cuando toouse

Hay dos casos de uso específicos cuando resulta útil tooblock Hola centro de IoT los puntos de conexión para determinadas direcciones IP:

- IoT Hub debe recibir tráfico solo de un intervalo concreto de direcciones IP y rechazar todo lo demás. Por ejemplo, se utiliza el centro de IoT con [Azure Express Route] toocreate conexiones privadas entre un centro de IoT y su infraestructura local.
- Necesita tooreject tráfico de direcciones IP que se han identificado como sospechosa por administrador de base de datos central de hello IoT.

## <a name="how-filter-rules-are-applied"></a>Cómo se aplican las reglas de filtro

se aplican las reglas de filtro IP de Hello en Hola de nivel de servicio del centro de IoT. Por lo tanto, las reglas de filtro IP de hello aplican las conexiones de tooall desde dispositivos y aplicaciones de back-end mediante un protocolo admitido.

Cualquier intento de conexión desde una dirección IP que coincida con una regla IP de rechazo en su centro de IoT recibe un código de estado 401 no autorizado y la descripción. mensaje de respuesta de Hello no mencione la regla IP de Hola.

## <a name="default-setting"></a>Configuración predeterminada

De forma predeterminada, Hola **filtro IP** cuadrícula en el portal de Hola para un centro de IoT está vacío. Esta configuración predeterminada significa que el centro de acepta la conexión de cualquier dirección IP. Esta configuración predeterminada es la regla de tooa equivalente que acepta el intervalo de direcciones IP de hello 0.0.0.0/0.

![Configuración predeterminada de filtro de direcciones IP de IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Incorporación o edición de una regla de filtro IP

Cuando se agrega una regla de filtrado IP, le pediremos Hola siguientes valores:

- Un **nombre de regla de filtro IP** que debe ser una cadena única, entre mayúsculas y minúsculas, alfanumérica seguridad too128 caracteres. Solo caracteres alfanuméricos de hello ASCII 7 bits más `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` se aceptan.
- Seleccione un **rechazar** o **Aceptar** como hello **acción** para regla de filtrado IP de Hola.
- Proporcione una única dirección IPv4 o un bloque de direcciones IP en la notación CIDR. Por ejemplo, en CIDR notación 192.168.100.0/22 representa las direcciones IPv4 Hola 1024 de 192.168.100.0 too192.168.103.255.

![Agregar un centro de IoT IP tooan de regla de filtro][img-ip-filter-add-rule]

Después de guardar la regla de hello, verá una alerta que le avise que esa actualización Hola está en curso.

![Notificación acerca de cómo guardar una regla de filtro IP][img-ip-filter-save-new-rule]

Hola **agregar** opción está deshabilitada cuando se alcanza el máximo de Hola de 10 reglas de filtrado IP.

Puede editar una regla existente haciendo doble clic en la fila de Hola que contiene la regla de Hola.

> [!NOTE]
> Rechazar IP direcciones pueden impedir que otros servicios de Azure (por ejemplo, análisis de transmisiones de Azure, máquinas virtuales de Azure o hello explorador del dispositivo en el portal de hello) interactuar con el centro de IoT Hola.

> [!WARNING]
> Si usa mensajes de tooread de análisis de transmisiones de Azure (ASA) de un centro de IoT con filtrado de IP habilitada, utilizar nombre de concentrador de eventos-compatible de Hola y el extremo de su centro de IoT Hola cadena de conexión del ASA.

## <a name="delete-an-ip-filter-rule"></a>Eliminación de una regla de filtro IP

toodelete una regla de filtro IP, seleccione una o varias reglas en la cuadrícula de Hola y haga clic en **eliminar**.

![Eliminación de una regla de filtro IP de IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Evaluación de las reglas de filtro IP

Se aplican las reglas de filtro IP en orden y primera regla Hola de esa dirección IP de coincidencias Hola determina Hola Aceptar o rechazar la acción.

Por ejemplo, si desea direcciones tooaccept en hello intervalo 192.168.100.0/22 y todo lo demás rechazar, Hola primera regla cuadrícula Hola debe aceptar Hola dirección intervalo 192.168.100.0/22. regla siguiente Hola debe rechazar todas las direcciones mediante el uso de intervalo de hello 0.0.0.0/0.

Puede cambiar el orden de Hola de las reglas de filtrado IP en la cuadrícula de hello haciendo clic en hello tres puntos verticales situados al principio de Hola de una fila y mediante arrastrar y colocar.

filtrar de la IP nueva toosave orden de reglas, haga clic en **guardar**.

![Cambiar el orden de Hola de las reglas de filtrado de IP del centro de IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a>Pasos siguientes

toofurther explorar las capacidades de Hola de centro de IoT, vea:

- [Supervisión de operaciones][lnk-monitor]
- [Métricas de IoT Hub][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md