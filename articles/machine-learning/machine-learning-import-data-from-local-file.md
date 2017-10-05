---
title: "Importación de datos desde un archivo en Azure Machine Learning Studio | Microsoft Docs"
description: "Obtenga información sobre cómo cargar un archivo de datos de entrenamiento desde la unidad de disco duro a Azure Machine Learning Studio. Esto crea un módulo de conjunto de datos en el área de trabajo."
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
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="a6cbd-105">Importar datos de entrenamiento desde un archivo en la unidad de disco duro en Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="a6cbd-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="a6cbd-106">Obtenga información sobre cómo cargar un archivo de datos desde la unidad de disco duro para usar como datos de entrenamiento en Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="a6cbd-107">Al importar el archivo de datos, dispone de un módulo de conjunto de datos listo para su uso en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="a6cbd-108">Pasos para importar datos desde un archivo local</span><span class="sxs-lookup"><span data-stu-id="a6cbd-108">Steps to import data from a local file</span></span>
<span data-ttu-id="a6cbd-109">Para importar datos desde una unidad de disco duro local, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a6cbd-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="a6cbd-110">Haga clic en **+NUEVO** en la parte inferior de la ventana de Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="a6cbd-111">Seleccione **CONJUNTO DE DATOS** y **DESDE ARCHIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="a6cbd-112">En el cuadro de diálogo **Cargar un nuevo conjunto de datos** , vaya al archivo que desea cargar.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="a6cbd-113">Escriba un nombre, identifique el tipo de datos y, si lo desea, escriba una descripción.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="a6cbd-114">Se recomienda incluir una descripción: le permite registrar cualquier característica acerca de los datos que quiera recordar cuando use los datos en el futuro.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="a6cbd-115">La casilla **Esta es la versión nueva de un conjunto de datos existente** le permite actualizar una base de datos existente con datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="a6cbd-116">Haga clic en esta casilla y, después, escriba el nombre de un conjunto de datos existente.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Carga de un conjunto de datos nuevo](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="a6cbd-118">Durante la carga, verá un mensaje que le indica que se está cargando el archivo.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="a6cbd-119">El tiempo de la carga dependerá del tamaño de los datos y de la velocidad de conexión con el servicio.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="a6cbd-120">Si sabe que el archivo tardará mucho tiempo en cargarse, puede realizar otras operaciones en Estudio de aprendizaje automático mientras espera.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="a6cbd-121">Sin embargo, si cierra el explorador, la carga de los datos genera un error.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="a6cbd-122">Módulo de conjunto de datos listo para usarse</span><span class="sxs-lookup"><span data-stu-id="a6cbd-122">Dataset module is ready for use</span></span>
<span data-ttu-id="a6cbd-123">Una vez que los datos estén cargados, se almacenan en un módulo de conjunto de datos y se encontrarán disponibles para cualquier experimento que se realice en su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="a6cbd-124">Cuando edita un experimento, puede encontrar los conjuntos de datos que ha creado en la lista **My Datasets** (Mis conjuntos de datos) que aparece en la lista **Saved Datasets** (Conjuntos de datos guardados) en la paleta de módulos.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="a6cbd-125">Puede arrastrar y colocar el conjunto de datos en el lienzo de experimento cuando desee usarlo para profundizar en su análisis o para Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a6cbd-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
