---
title: "un servicio Web de aprendizaje de máquina desde Excel aaaConsume | Documentos de Microsoft"
description: "Consumir un servicio web de Aprendizaje automático de Azure de Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Consumo de un servicio web de Aprendizaje automático de Azure de Excel
 Estudio de aprendizaje automático de Azure hace fácil toocall los servicios web directamente desde Excel sin Hola necesita toowrite cualquier código.

Si utiliza Excel 2013 (o posterior) o Excel Online, se recomienda que use Excel hello [complemento de Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Pasos
Publicar un servicio web. [Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica cómo toodo lo. Actualmente la característica de libro de Excel de hello solo se admite para los servicios de solicitud/respuesta que tienen una salida única (es decir, una etiqueta de puntuación única). 

Una vez que tenga un servicio web, haga clic en hello **servicios WEB** sección izquierda Hola de studio hello y, a continuación, seleccione tooconsume de servicio web de Hola desde Excel.

**Servicio web clásico**

1. En hello **panel** ficha servicio web de hello es una fila para hello **solicitud/respuesta** servicio. Si este servicio tiene una salida única, debería ver Hola **descargar el libro de Excel** vínculo en esa fila.
   
    ![][1]
2. Haga clic en **Descargar el libro de Excel**.

**Servicio web nuevo**

1. En el portal de servicio Web de Azure Machine Learning hello, seleccione **usar**.
2. En página de consumir hello, Hola **opciones de consumo del servicio Web** sección, haga clic en el icono de Excel de Hola.

**Utilizando el libro de Hola**

1. Libro de hello abierto.
2. Aparece una advertencia de seguridad; Haga clic en hello **Habilitar edición** botón.
   
    ![][2]
3. Aparecerá una advertencia de seguridad. Haga clic en hello **Habilitar contenido** botón toorun macros en la hoja de cálculo.
   
    ![][3]
4. Una vez que las macros están habilitadas, se generará una tabla. Columnas en azul son necesarias como entrada en hello servicio web de RR, o **parámetros**. Tenga en cuenta la salida de hello de hello servicio RR, **valores PREDICHOS** en verde. Cuando se llenan todas las columnas de una fila determinada, libro Hola llama Hola API de puntuación y muestra hello resultados puntuado.
   
    ![][4]
5. tooscore más de una fila, la segunda fila de Hola de relleno con los datos y Hola predecir se generan los valores. Incluso puede pegar varias filas a la vez.

Puede usar cualquiera de las características de Excel hello (gráficos, asignación de energía, condicional formato, etc.) con hello predicha valores toohelp visualizar datos de Hola.    

## <a name="sharing-your-workbook"></a>Compartir el libro
Para hello macros toowork, la clave de API debe formar parte de la hoja de cálculo de Hola. Que significa que deben compartir libro Hola únicamente con personas o entidades de confianza.

## <a name="automatic-updates"></a>Actualizaciones automáticas
En las siguientes dos situaciones se realiza una llamada a RRS:

1. Hola la primera vez que una fila tiene contenido en todos sus **parámetros**
2. Cada vez que cualquiera de hello **parámetros** cambios en una fila que tenían todos sus **parámetros** especificado.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
