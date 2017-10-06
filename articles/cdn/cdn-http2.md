---
title: compatibilidad con aaaHTTP/2 en la red CDN de Azure | Documentos de Microsoft
description: Aprenda sobre la compatibilidad con HTTP/2 y la red CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Compatibilidad con HTTP/2 en la red CDN de Azure

HTTP/2 es una tooHTTP/1.1\ revisión principal. Proporciona más rápido experimentan usuario mejorada, tiempo de respuesta reducido y rendimiento web, al tiempo que mantiene los métodos HTTP conocidos de hello, códigos de estado y la semántica. Aunque HTTP/2 es toowork diseñada con HTTP y HTTPS, muchos exploradores web de cliente solo son compatibles con HTTP/2 a través de TLS.

###<a name="http2-benefits"></a>Ventajas HTTP/2

ventajas de Hola de HTTP/2 incluyen:

*   **Multiplexación y simultaneidad**

    Mediante HTTP 1.1, para realizar varias solicitudes de varios recursos se requieren varias conexiones TCP y cada conexión tiene asociada una sobrecarga de rendimiento. HTTP/2 permite que varios toobe recursos solicitado en una sola conexión de TCP.

*   **Compresión de encabezados**

    Mediante la compresión de encabezados de hello HTTP para recursos atendidos, tiempo en conexión Hola se reduce significativamente.

*   **Dependencias de secuencias**

    Dependencias de secuencia permiten a cliente hello tooindicate toohello server qué recursos tienen prioridad.


##<a name="http2-browser-support"></a>Compatibilidad con exploradores HTTP/2

Todos los exploradores principales de hello han implementado la compatibilidad con HTTP/2 en sus versiones actuales. Los exploradores no compatibles tendrán automáticamente reserva tooHTTP/1.1.

|Browser|Versión mínima|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Habilitación de la compatibilidad con HTTP/2 en la red CDN de Azure

La compatibilidad con HTTP/2 se encuentra actualmente activa para los perfiles de **red CDN de Azure de Akamai** y la **red CDN de Azure de Verizon**. No es necesaria ninguna otra acción por parte de los clientes.

##<a name="next-steps"></a>Pasos siguientes

ventajas de hello toosee de HTTP/2 en acción, vea [esta demostración de Akamai](https://http2.akamai.com/demo).

toolearn más información acerca de HTTP/2, visite Hola recursos siguientes:

*   [Página principal de especificación de HTTP/2](https://http2.github.io/)
*   [Preguntas más frecuentes oficiales de HTTP/2](https://http2.github.io/faq/)
*   [Información de HTTP/2 de Akamai](https://http2.akamai.com/)

toolearn más información acerca de funciones disponibles en de CDN de Azure, vea hello [información general sobre la red CDN de Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).
