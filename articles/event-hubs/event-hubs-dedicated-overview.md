---
title: aaaOverview de la capacidad de los centros de eventos de Azure dedicado | Documentos de Microsoft
description: "Introducción a la capacidad dedicada de Microsoft Azure Event Hubs."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Introducción a Event Hubs dedicado

*Concentradores de eventos dedicado* capacidad ofrece único inquilino implementaciones para los clientes con hello requisitos más exigentes. A escala completa, los concentradores de eventos de Azure puede entrada más de 2 millones eventos por segundo o backup too2 GB por segundo de telemetría con una latencia de almacenamiento y fracciones de segundos totalmente durable. Este también permite soluciones integradas mediante el procesamiento en tiempo real y el lote en Hola mismo sistema. Con el archivado de los centros de eventos incluidos en la oferta de hello, puede reducir la complejidad de hello de la solución al tener un único flujo admite canalizaciones en tiempo real y basadas en lotes.

Hello tabla siguiente comparan los niveles de servicio disponible de Hola de centros de eventos. oferta de Hello dedicado de concentradores de eventos es un precio mensual fijo, comparado toousage precios para la mayoría de las características de Standard y Basic. nivel dedicado Hola ofrece características de hello del plan estándar hello, pero con capacidad de escala de empresa para clientes con exigentes cargas de trabajo. 

| Característica | Básico | Estándar | Dedicado |
| --- |:---:|:---:|:---:|
| Eventos de entrada | Pago por millones de eventos | Pago por millones de eventos | Se incluye |
| Unidad de rendimiento (entrada de 1 MB/seg., salida de 2 MB/seg.) | Pago por hora | Pago por hora | Se incluye |
| Tamaño de los mensajes | 256 KB | 256 KB | 1 MB |
| Directivas de publicadores | N/D | Sí | Sí |     
| Grupos de consumidores | 1: predeterminado | 20 | 20 | |
| Redifusión de mensajes | Sí | Sí | Sí |
| Unidades de rendimiento máximo | 20 | | 20 (too100 flexible)  | 1 CU≈200 |
| Conexiones asincrónicas | 100 incluidos | 1000 incluidos | 100 000 incluidos |
| Conexiones desacopladas adicionales | N/D | Sí | Sí |
| Retención de mensajes | 1 día incluido | 1 día incluido | Una copia de seguridad too7 días incluido |
| Archive(Versión preliminar) | N/D   | Pago por hora | Se incluye |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Ventajas de Event Hubs con capacidad dedicada

Hola después ventajas está disponible al utilizar dedicado de concentradores de eventos:

* Hospedaje de un solo inquilino sin ruido de otros inquilinos.
* Mensaje aumenta de tamaño too1 MB en comparación too256 KB para Standard Edition y Basic.
* Rendimiento repetible cada vez.
* Se garantiza que toomeet de capacidad que necesita la ráfaga.
* Escalable entre 1 y las unidades de capacidad 8 (CU): proporcionar eventos de entrada millones de too2 por segundo.
  * Perso administra el escalado de Hola para dedicado para los centros de eventos, donde cada CU puede proporcionar aproximadamente el equivalente de hello 200 unidades de rendimiento (MA).
* Cero mantenimiento: nosotros administramos el equilibrio de carga, las actualizaciones del sistema operativo, las revisiones de seguridad y la creación de particiones.
* Precio fijo mensual.

Dedicado de concentradores de eventos también quita algunas de las limitaciones de rendimiento de Hola de oferta estándar Hola. Unidades de rendimiento en los niveles básico y estándar autorizar a too1000 eventos por segundo o 1 MB por segundo de entrada por TU y double esa cantidad de salida. oferta de escala dedicado Hello no tiene ninguna restricción en la entrada y recuentos de eventos de salida. Estos límites se rigen solo por la capacidad de hello adquirido los concentradores de eventos de procesamiento de Hola.

Este servicio está destinada a los usuarios de telemetría mayor hello y toocustomers disponible con un contrato enterprise.

## <a name="how-tooonboard"></a>Cómo tooonboard

plataforma de Hello dedicado de concentradores de eventos se ofrece a través de un contrato enterprise con diferentes tamaños de Perso. Cada CU proporciona aproximadamente el Hola equivalente de 200 unidades de rendimiento. Puede escalar la capacidad hacia arriba o hacia abajo a lo largo de hello mes toomeet sus necesidades agregando o quitando Perso. plan dedicado Hello es único en que experimenta una incorporación más práctica de hello centros de eventos producto equipo tooget Hola implementación flexible que es adecuado para usted. 

## <a name="next-steps"></a>Pasos siguientes
Póngase en contacto con su representante de ventas de Microsoft o Microsoft Support tooget obtener más detalles acerca de la capacidad de dedicado de concentradores de eventos. También puede aprender más acerca de los centros de eventos visitando Hola siguientes vínculos:

Para obtener información detallada sobre los precios, visite Hola siguientes vínculos:

- [Precios de Event Hubs dedicado](https://azure.microsoft.com/pricing/details/event-hubs/). También puede establecer contacto con su representante de ventas de Microsoft o Microsoft Support tooget obtener detalles adicionales sobre capacidad dedicado de concentradores de eventos.
- Hola [preguntas más frecuentes de los centros de eventos](event-hubs-faq.md) contiene información sobre los precios y responde a algunas preguntas frecuentes acerca de los centros de eventos. 
