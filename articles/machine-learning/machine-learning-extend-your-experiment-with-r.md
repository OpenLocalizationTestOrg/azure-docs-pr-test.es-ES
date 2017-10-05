---
title: Extender el experimento con R | Microsoft Docs
description: "Cómo extender la funcionalidad de Estudio de aprendizaje automático de Azure mediante el lenguaje R con el módulo Ejecutar script de R."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="a7954-103">Extender el experimento con R</span><span class="sxs-lookup"><span data-stu-id="a7954-103">Extend your experiment with R</span></span>
<span data-ttu-id="a7954-104">Puede extender la funcionalidad de Azure Machine Learning Studio mediante el lenguaje R con el módulo [Ejecutar script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a7954-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a7954-105">Este módulo acepta varios conjuntos de datos de entrada y genera un solo conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="a7954-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="a7954-106">Puede escribir un script de R en el parámetro **Script de R** del módulo [Ejecutar script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a7954-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a7954-107">Para tener acceso a cada puerto de entrada del módulo, se usa un código similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a7954-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="a7954-108">Enumeración de todos los paquetes actualmente instalados</span><span class="sxs-lookup"><span data-stu-id="a7954-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="a7954-109">La lista de paquetes instalados puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="a7954-109">The list of installed packages can change.</span></span> <span data-ttu-id="a7954-110">Puede encontrar una lista de los paquetes instalados actualmente en [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Paquetes de R compatibles con Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="a7954-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="a7954-111">También puede obtener la lista completa y actual de los paquetes instalados especificando el código siguiente en el módulo [Ejecutar script de R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="a7954-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="a7954-112">Esto acción envía la lista de paquetes al puerto de salida del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a7954-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="a7954-113">Para ver la lista de paquetes, conecte un módulo de conversión, como [Convertir a CSV][convert-to-csv] con la salida izquierda del módulo [Ejecutar script R][execute-r-script], ejecute el experimento y luego haga clic en la salida del módulo de conversión y seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="a7954-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![Descarga de los resultados del módulo Convertir en CSV](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="a7954-115">Importación de paquetes</span><span class="sxs-lookup"><span data-stu-id="a7954-115">Importing packages</span></span>
<span data-ttu-id="a7954-116">Puede importar paquetes que no se hayan instalado mediante el uso de los siguientes comandos en el módulo [Ejecutar script de R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="a7954-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="a7954-117">donde el archivo `my_favorite_package.zip` contiene el paquete.</span><span class="sxs-lookup"><span data-stu-id="a7954-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
