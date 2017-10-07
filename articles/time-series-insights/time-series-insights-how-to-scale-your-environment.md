---
title: "aaaHow tooscale el entorno de visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "Este tutorial trata cómo tooscale su entorno de visión de serie de tiempo de Azure"
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
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Cómo tooscale su entorno de visión de la serie de tiempo

Este tutorial trata cómo tooscale su entorno de visión de la serie de tiempo.

> [!NOTE]
> No se permite el escalado vertical entre los tipos de SKU. Un entorno con una SKU S1 no se puede convertir en un entorno de S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>Capacidades y tasas de entrada de SKU de S1

| Capacidad de SKU de S1 | Velocidad de entrada | Capacidad máxima de almacenamiento
| --- | --- | --- |
| 1 | 1 GB (1 millones de eventos) | 30 GB (30 millones de eventos) al mes |
| 10 | 10 GB (10 millones de eventos) | 300 GB (300 millones de eventos) al mes |

## <a name="s2-sku-ingress-rates-and-capacities"></a>Capacidades y tasas de entrada de SKU de S2

| Capacidad de SKU de S2 | Velocidad de entrada | Capacidad máxima de almacenamiento
| --- | --- | --- |
| 1 | 10 GB (10 millones de eventos) | 300 GB (300 millones de eventos) al mes |
| 10 | 100 GB (100 millones de eventos) | 3 TB (3 mil millones de eventos) al mes |

Las capacidades se escalan linealmente, por lo que una SKU de S1 con capacidad 2 admite una tasa de entrada de 2 GB (2 millones) de eventos al día y 60 GB (60 millones de eventos) al mes.

## <a name="changing-hello-capacity-of-your-environment"></a>Cambiar la capacidad de Hola de su entorno

1. Hola portal de Azure, seleccione Hola entorno cuya capacidad desea toochange.
1. En Configuración, haga clic en Configurar.
1. Utilice Hola capacidad control deslizante tooselect Hola capacidad que cumpla los requisitos de Hola para las tarifas de entrada y almacenamiento.

## <a name="next-steps"></a>Pasos siguientes

* Compruebe que la nueva capacidad de hello es suficiente tooprevent limitación. Para obtener más información, vea hello *el entorno podría obtener limitarán* sección [aquí](time-series-insights-diagnose-and-solve-problems.md).
