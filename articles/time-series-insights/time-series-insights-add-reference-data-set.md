---
title: "entorno de visión de serie de tiempo de Azure de tooyour del conjunto de datos de referencia de aaaAdd | Documentos de Microsoft"
description: "En este tutorial, agregará un entorno de visión de la serie de tiempo de tooyour de conjunto de datos de referencia"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Crear un conjunto de datos de referencia para su entorno de visión de la serie de tiempo mediante este portal como Hola

Un conjunto de datos de referencia es una colección de elementos que se han aumentado con eventos de Hola desde el origen del evento. El motor de entrada de Time Series Insights une a un evento del origen de eventos con un elemento en el conjunto de datos de referencia. A partir de ese momento, este evento aumentado está disponible para consultas. Esta combinación se basa en claves de hello definidas en el conjunto de datos de referencia.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Pasos tooadd un entorno de tooyour del conjunto de datos de referencia

1. Inicie sesión en toohello [este portal como](https://portal.azure.com).
2. Haga clic en "Todos los recursos" en el menú izquierda Hola de este portal como Hola Hola.
3. Seleccione el entorno de Time Series Insights.

    ![Crear conjunto de datos de referencia de hello visión de la serie de tiempo](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Seleccione "Conjuntos de datos de referencia" y haga clic en "+ Agregar".

    ![Crear conjunto de datos de referencia de visión de la serie de tiempo hello - detalles](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Especifique el nombre de Hola Hola referencia del conjunto de datos.
6. Especifique el nombre de clave de Hola y su tipo. Este nombre y el tipo es propiedad correcto de Hola de toopick usado del evento de hello en el origen del evento. Por ejemplo, si proporciona el nombre de clave como "DeviceId" y el tipo como "String", a continuación, Hola visión de serie de tiempo de motor de entrada busca una propiedad con nombre hello "DeviceId" de tipo "String" en el evento de entrada de Hola. Puede proporcionar más de un toojoin clave con eventos de Hola. coincidencia de nombre de propiedad de Hello distingue mayúsculas de minúsculas.

     ![Crear conjunto de datos de referencia de visión de la serie de tiempo hello - detalles](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Haga clic en "Crear".

## <a name="next-steps"></a>Pasos siguientes

* [Administración de datos de referencia](time-series-insights-manage-reference-data-csharp.md) mediante programación.
* Para la referencia de API completa de hello, consulte [API de datos de referencia](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.
