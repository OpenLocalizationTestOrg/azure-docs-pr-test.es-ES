---
title: "aaaImport datos de un archivo en estudio de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupload datos de entrenamiento de archivos desde su tooAzure de unidad de disco duro estudio de aprendizaje automático. Esto crea un módulo de conjunto de datos en el área de trabajo de Hola."
keywords: "importar datos, formato de datos, tipos de datos, orígenes de datos, datos de entrenamiento"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importar datos de entrenamiento desde un archivo en la unidad de disco duro en Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Obtenga información acerca de cómo tooupload datos de un archivo de la unidad de disco duro toouse como datos de entrenamiento en estudio de aprendizaje automático de Azure. Al importar el archivo de datos de hello, dispone de un módulo de conjunto de datos listo para su uso en el área de trabajo.

## <a name="steps-tooimport-data-from-a-local-file"></a>Datos de tooimport pasos desde un archivo local
Hola tooimport datos desde una unidad de disco duro local, después de:

1. Haga clic en **+ nuevo** final Hola de ventana de estudio de aprendizaje automático de hello.
2. Seleccione **CONJUNTO DE DATOS** y **DESDE ARCHIVO LOCAL**.
3. Hola **cargar un nuevo conjunto de datos** cuadro de diálogo, archivo de toohello de examen que desee tooupload
4. Escriba un nombre, identifique el tipo de datos de hello y, opcionalmente, escriba una descripción. Se recomienda una descripción: le permite toorecord características acerca de los datos de Hola que desea tooremember cuando se usan datos de hello en el futuro de Hola.
5. Hola casilla **es Hola nueva versión de un conjunto de datos existente** permite tooupdate un conjunto de datos existente con nuevos datos. Haga clic en esta casilla de verificación y, a continuación, escriba nombre de Hola de un conjunto de datos existente.

![Carga de un conjunto de datos nuevo](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Durante la carga, verá un mensaje que le indica que se está cargando el archivo. Cargar tiempo depende de tamaño de hello de la velocidad de hello y datos de su servicio de toohello de conexión. Si conoce el archivo hello tardará mucho tiempo, puede hacer otras cosas en estudio de aprendizaje automático mientras espera. Sin embargo, cierre el Explorador de hello hace toofail de carga de datos de Hola.

## <a name="dataset-module-is-ready-for-use"></a>Módulo de conjunto de datos listo para usarse
Una vez que se cargan los datos, se almacena en un módulo de conjunto de datos y es experimento tooany disponible en el área de trabajo.

Cuando se edita un experimento, puede encontrar Hola conjuntos de datos que ha creado en hello **Mis conjuntos de datos** lista bajo hello **conjuntos de datos guardados** lista en la paleta de módulo de Hola. Puede arrastrar y drop Hola dataset al lienzo del experimento de hello cuando desee que el conjunto de datos de toouse hello para el análisis adicional y aprendizaje automático.
