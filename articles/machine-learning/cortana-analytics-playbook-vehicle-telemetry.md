---
title: "Mantenimiento de vehículo aaaPredict y dirigir hábitos - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Cuaderno de estrategias de soluciones de análisis de telemetría de vehículo
Esto **menú** vincula toohello capítulos en esta guía. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Información general
Equipos superusuarios han movido fuera del laboratorio de Hola y ahora están aparcados en nuestros artículos! Estos automóviles vanguardistas contienen una gran cantidad de sensores, darles tootrack de capacidad de Hola y supervisar millones de eventos por segundo. Esperamos que por 2020, la mayoría de estos coches habrá sido toohello conectado Internet. ¡Imagine pulsar en esta gran cantidad de datos tooprovide mayor seguridad, confiabilidad y una experiencia mejor determinante! Microsoft ha convertido ese sueño en una realidad gracias a Cortana Intelligence.

Inteligencia de Cortana de Microsoft es una grande de datos totalmente administrado y avanzado conjunto de análisis que permite tootransform los datos en acción inteligente. Queremos toointroduce toohello plantilla de solución de análisis de telemetría de Cortana Intelligence vehículo. Esta solución muestra cómo concesiones de coches, los fabricantes de automóviles y compañías de seguros pueden usar las capacidades de Hola de inteligencia de Cortana toogain en tiempo real y transformación de la visión de predicción en mantenimiento de vehículo y dirigir. 

solución de Hola se implementa como un [lambda (modelo) arquitectura](https://en.wikipedia.org/wiki/Lambda_architecture) que muestra todas las posibilidades de plataforma de inteligencia de Cortana de Hola para hello en tiempo real y procesamiento por lotes. solución de Hello: 

* Proporcionar un simulador telemático de vehículo
* Utilizar Event Hubs para la introducción de millones de eventos de telemetría de vehículo en Azure 
* usa la información de análisis de transmisiones toogain en tiempo real en el estado del vehículo
* conserva los datos de hello en el almacenamiento a largo plazo para el análisis de lote más rica. 
* aprovecha las ventajas de aprendizaje automático para la detección de anomalías de en tiempo real y procesamiento toogain predictivo visión de lote.
* aprovecha los datos de tootransform de HDInsight en la escala y orquestación toohandle de factoría de datos, programación, administración de recursos y supervisión de canalización de procesamiento por lotes de Hola 
* Ofrecer a esta solución un panel completo de datos en tiempo real y visualizaciones de análisis predictivo mediante Power BI

## <a name="architecture"></a>Arquitectura
![Diagrama de la arquitectura de la solución](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1: Arquitectura de la solución de análisis de telemetría de vehículos*

Esta solución incluye siguiente hello **componentes Cortana Intelligence** y muestra su integración de tooend final:

* **Centros de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.
* **Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.
* **Aprendizaje automático** para la detección de anomalías en tiempo real y toogain predictiva visión de procesamiento por lotes.
* **HDInsight** tootransform aprovechado datos a escala
* **Factoría de datos** controla la orquestación, programación, administración de recursos y la supervisión de la canalización de procesamiento por lotes de Hola.
* **Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.

Esta solución tiene acceso a dos **orígenes de datos**diferentes: 

* **Simular las señales de vehículo y diagnóstico**: un simulador de telemáticas vehículo emite información de diagnóstico y las señales que corresponden toohello estado del vehículo de Hola y Hola automóvil patrón en un momento dado en el tiempo. 
* **Catálogo de vehículo**: un conjunto de datos de referencia que contiene una asignación de toomodel Niv.

