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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="5c820-105">Importar datos de entrenamiento desde un archivo en la unidad de disco duro en Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5c820-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="5c820-106">Obtenga información acerca de cómo tooupload datos de un archivo de la unidad de disco duro toouse como datos de entrenamiento en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c820-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="5c820-107">Al importar el archivo de datos de hello, dispone de un módulo de conjunto de datos listo para su uso en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5c820-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="5c820-108">Datos de tooimport pasos desde un archivo local</span><span class="sxs-lookup"><span data-stu-id="5c820-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="5c820-109">Hola tooimport datos desde una unidad de disco duro local, después de:</span><span class="sxs-lookup"><span data-stu-id="5c820-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="5c820-110">Haga clic en **+ nuevo** final Hola de ventana de estudio de aprendizaje automático de hello.</span><span class="sxs-lookup"><span data-stu-id="5c820-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="5c820-111">Seleccione **CONJUNTO DE DATOS** y **DESDE ARCHIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="5c820-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="5c820-112">Hola **cargar un nuevo conjunto de datos** cuadro de diálogo, archivo de toohello de examen que desee tooupload</span><span class="sxs-lookup"><span data-stu-id="5c820-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="5c820-113">Escriba un nombre, identifique el tipo de datos de hello y, opcionalmente, escriba una descripción.</span><span class="sxs-lookup"><span data-stu-id="5c820-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="5c820-114">Se recomienda una descripción: le permite toorecord características acerca de los datos de Hola que desea tooremember cuando se usan datos de hello en el futuro de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c820-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="5c820-115">Hola casilla **es Hola nueva versión de un conjunto de datos existente** permite tooupdate un conjunto de datos existente con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="5c820-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="5c820-116">Haga clic en esta casilla de verificación y, a continuación, escriba nombre de Hola de un conjunto de datos existente.</span><span class="sxs-lookup"><span data-stu-id="5c820-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Carga de un conjunto de datos nuevo](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="5c820-118">Durante la carga, verá un mensaje que le indica que se está cargando el archivo.</span><span class="sxs-lookup"><span data-stu-id="5c820-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="5c820-119">Cargar tiempo depende de tamaño de hello de la velocidad de hello y datos de su servicio de toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="5c820-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="5c820-120">Si conoce el archivo hello tardará mucho tiempo, puede hacer otras cosas en estudio de aprendizaje automático mientras espera.</span><span class="sxs-lookup"><span data-stu-id="5c820-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="5c820-121">Sin embargo, cierre el Explorador de hello hace toofail de carga de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c820-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="5c820-122">Módulo de conjunto de datos listo para usarse</span><span class="sxs-lookup"><span data-stu-id="5c820-122">Dataset module is ready for use</span></span>
<span data-ttu-id="5c820-123">Una vez que se cargan los datos, se almacena en un módulo de conjunto de datos y es experimento tooany disponible en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5c820-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="5c820-124">Cuando se edita un experimento, puede encontrar Hola conjuntos de datos que ha creado en hello **Mis conjuntos de datos** lista bajo hello **conjuntos de datos guardados** lista en la paleta de módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c820-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="5c820-125">Puede arrastrar y drop Hola dataset al lienzo del experimento de hello cuando desee que el conjunto de datos de toouse hello para el análisis adicional y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="5c820-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
