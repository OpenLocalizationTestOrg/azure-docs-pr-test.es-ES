---
title: aaaSecure su Internet de las cosas (IoT) en Azure | Documentos de Microsoft
description: " Los servicios de Internet de las cosas (IoT) de Azure ofrecen una amplia gama de funcionalidades. En este artículo le ayudará a comprender cómo toosecure sus soluciones de IoT de Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Información general sobre seguridad de Internet de las cosas
Los servicios de Internet de las cosas (IoT) de Azure ofrecen una amplia gama de funcionalidades. Estos servicios de nivel empresarial le permiten:

* Recopilar datos de dispositivos
* Analizar flujos de datos en movimiento
* Almacenar y consultar grandes conjuntos de datos
* Visualizar datos tanto históricos como en tiempo real
* Integración con sistemas del área de operaciones

toodeliver estas capacidades, conjunto de IoT de Azure incorpora varios servicios de Azure con las extensiones personalizadas como soluciones preconfiguradas. Estas soluciones preconfiguradas son implementaciones base de patrones comunes de solución de IoT que ayudan a la hora de hello tooreduce que tomar toodeliver sus soluciones de IoT. Kits de desarrollo de software de hello IoT puede personalizar y extender estas soluciones toomeet sus propios requisitos. También puede usar estas soluciones como ejemplos o plantillas al desarrollar nuevas soluciones de IoT.

conjunto de Hello IoT de Azure es una potente solución para sus necesidades de IoT. Sin embargo, resulta de importancia lo que más que las soluciones de IoT están diseñadas teniendo en cuenta de inicio de Hola la seguridad. Debido a número total de Hola de dispositivos de IoT, cualquier incidente de seguridad puede volverse rápidamente un evento generalizado con consecuencias significativas.

toohelp que comprenda cómo toosecure sus soluciones de IoT, tenemos Hola siguiente información.

## <a name="security-architecture"></a>Arquitectura de seguridad
Al diseñar un sistema, es importante toounderstand las amenazas potenciales de hello toothat sistema y agregar las defensas adecuadas según corresponda, como sistema de hello está diseñado y está diseñado. Es importante toodesign Hola producto desde el principio de hello teniendo en cuenta la seguridad debido a que comprender cómo un atacante podría ser capaz de toocompromise un sistema de ayuda a asegurarse de que las mitigaciones adecuadas están en vigor desde el principio de Hola.

Puede consultar [Arquitectura de seguridad de Internet de las cosas](../iot-suite/iot-security-architecture.md)para obtener información sobre la arquitectura de seguridad de IoT.

En este artículo se describe Hola temas siguientes:

* [La seguridad comienza con un modelo de riesgos](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Seguridad de IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Hola de modelado de amenaza para la arquitectura de referencia de IoT de Azure](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Seguridad de hello masa
Hola IoT plantea único seguridad, privacidad y cumplimiento desafíos toobusinesses en todo el mundo. A diferencia de la tecnología de intrusos tradicional donde estos problemas giran en torno a software y cómo se implementa, IoT está relacionado con lo que ocurre cuando los universos físico de Hola y Hola intrusos convergen. Proteger soluciones IoT requiere garantizar seguro de aprovisionamiento de dispositivos, una conexión segura entre estos dispositivos y la nube hello y la protección de proteger los datos en la nube de Hola durante el procesamiento y almacenamiento. Sin embargo, trabajar con esta funcionalidad tiene sus inconvenientes: la limitación de recursos de los dispositivos, la distribución geográfica de las implementaciones y la existencia de muchos dispositivos dentro de una solución.

Puede obtener información sobre cómo toohandle seguridad en estas áreas, lea [seguridad de Internet de las cosas de hello masa](../iot-suite/securing-iot-ground-up.md).

artículo de Hola trata Hola temas siguientes:

* [Infraestructura segura de hello masa](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure: infraestructura de IoT segura para su negocio](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Prácticas recomendadas
La protección de una infraestructura IoT requiere una estrategia de seguridad rigurosa y detallada. De la protección de datos en la nube de hello, proteger la integridad de los datos y en tránsito a través de hello pública internet, dispositivos de aprovisionamiento de toosecurely, cada capa basa mayor garantía de seguridad en toda la infraestructura de Hola.

Puede consultar [Procedimientos recomendados de seguridad de Internet de las cosas](../iot-suite/iot-security-best-practices.md)para conocer estos procedimientos recomendados.

artículo de Hola trata Hola temas siguientes:

* [Integrador/fabricante de hardware IoT](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Desarrollador de soluciones de IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Implementador de soluciones de IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Operador de soluciones de IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
