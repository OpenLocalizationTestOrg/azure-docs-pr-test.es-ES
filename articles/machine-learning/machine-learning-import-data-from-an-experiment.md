---
title: "Importación de datos en Machine Learning Studio desde otro experimento | Microsoft Docs"
description: "Cómo guardar los datos de aprendizaje en Estudio de aprendizaje automático de Azure y usarlo en otro experimento."
keywords: "importar datos, datos, orígenes de datos, datos de entrenamiento"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="349db-104">Importación de datos en Estudio de aprendizaje automático de Azure desde otro experimento</span><span class="sxs-lookup"><span data-stu-id="349db-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="349db-105">Habrá ocasiones en las que querrá tomar un resultado intermedio de un experimento y usarlo como parte de otro experimento.</span><span class="sxs-lookup"><span data-stu-id="349db-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="349db-106">Para ello, guarde el módulo como un conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="349db-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="349db-107">Haga clic en la salida del módulo que desea guardar como conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="349db-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="349db-108">Haga clic en **Guardar como conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="349db-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="349db-109">Cuando se le solicite, escriba un nombre y una descripción que le permitan identificar fácilmente el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="349db-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="349db-110">Haga clic en la marca de verificación **Aceptar** .</span><span class="sxs-lookup"><span data-stu-id="349db-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="349db-111">Cuando termine de guardar, el conjunto de datos estará disponible para usarlo dentro de cualquier experimento de su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="349db-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="349db-112">Puede encontrarlo en la lista **Conjuntos de datos guardados** de la paleta de módulos.</span><span class="sxs-lookup"><span data-stu-id="349db-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

