---
title: "Introducción a Azure IoT Suite aaaMicrosoft | Documentos de Microsoft"
description: "Información general sobre cómo Suite de IoT de Azure ofrece internet de las cosas soluciones preconfiguradas toocollect, analizar y almacenar los datos, proporcionar visualizaciones e integrar con otros sistemas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Información general de Azure IoT Suite

Hello Azure internet de servicios de las cosas (IoT) ofrecen una amplia gama de capacidades. Estos servicios de nivel empresarial le permiten:

* Recopilar datos de dispositivos
* Analizar flujos de datos en movimiento
* Almacenar y consultar grandes conjuntos de datos
* Visualizar datos tanto históricos como en tiempo real
* Integración con sistemas del área de operaciones
* Administración de los dispositivos

toodeliver estas capacidades, conjunto de IoT de Azure incorpora varios servicios de Azure con las extensiones personalizadas como *soluciones preconfiguradas*. Estas soluciones preconfiguradas son implementaciones base de patrones comunes de solución de IoT que ayudan a la hora de hello tooreduce que tomar toodeliver sus soluciones de IoT. Con hello [kits de desarrollo de software de IoT][lnk-sdks], puede personalizar y extender estos toomeet soluciones sus propios requisitos. También puede usar estas soluciones como ejemplos o plantillas al desarrollar nuevas soluciones de IoT.

Hello vídeo siguiente proporciona un conjunto de IoT tooAzure de introducción:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Servicios IoT de Azure en Azure IoT Suite
soluciones de Hello preconfigurado suelen usar Hola siguientes servicios:

* Core tooAzure IoT Suite es hello [centro de IoT de Azure] [ lnk-iot-hub] servicio. Este servicio proporciona Hola dispositivo a la nube y capacidades de mensajería de nube al dispositivo y actúa como Hola toohello de puerta de enlace en la nube y Hola otros servicios IoT Suite clave. servicio de Hello permite tooreceive mensajes desde los dispositivos a escala y enviar comandos tooyour dispositivos. Hola servicio también permite demasiado[administrar sus dispositivos][lnk-device-management]. Por ejemplo, puede configurar, reiniciar o realizar una restablecimiento de fábrica en Centro de toohello conectado uno o varios dispositivos.
* [Azure Stream Analytics][lnk-asa] ofrece análisis de datos en movimiento. IoT Suite utiliza esta telemetría entrantes tooprocess de servicio, realizar la agregación y detectar eventos. las soluciones de Hello preconfigurado también usan stream analytics tooprocess mensajes informativos que contienen datos como las respuestas de metadatos o el comando de dispositivos. soluciones de Hello utilizan mensajes de Hola tooprocess de análisis de transmisiones de los dispositivos y ofrecen servicios de tooother de esos mensajes.
* [Almacenamiento de Azure] [ lnk-azure-storage] y [base de datos de Azure Cosmos] [ lnk-document-db] proporcionan capacidades de almacenamiento de datos de Hola. Hello soluciones preconfiguradas usan telemetría de toostore de almacenamiento de blobs y toomake estén disponibles para su análisis. soluciones de Hello usan metadatos del dispositivo de base de datos de Cosmos toostore y habilitan las capacidades de administración del dispositivo de Hola de soluciones de Hola.
* [Las aplicaciones Web de Azure] [ lnk-web-apps] y [Microsoft Power BI] [ lnk-power-bi] proporcionan capacidades de visualización de datos de Hola. flexibilidad de Hola de Power BI permite tooquickly compilar sus propios paneles interactivos que utilizan datos de conjunto de IoT.

Para obtener información general de arquitectura de Hola de una solución de IoT típica, vea [hello Internet de las cosas (IoT) y Microsoft Azure][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>soluciones preconfiguradas

IoT Suite incluye las soluciones preconfiguradas que habilitar tooquickly empezar a trabajar con y tooexplore Hola IoT los escenarios comunes, como:

* Supervisión remota
* Mantenimiento predictivo
* Fábrica conectada

Puede implementar estos tooyour soluciones suscripción de Azure y, a continuación, ejecutar un escenario IoT completando-to-end.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene información general sobre lo que puede hacer IoT Suite y cuáles son sus componentes principales, se puede obtener más información sobre las soluciones de Hola preconfigurado en el conjunto de IoT. Para obtener más información, vea [¿qué hello Azure IoT soluciones preconfiguradas?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
