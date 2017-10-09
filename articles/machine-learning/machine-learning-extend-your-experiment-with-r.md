---
title: aaaExtend su experimento con R | Documentos de Microsoft
description: "La funcionalidad de hello tooextend de estudio de aprendizaje automático de Azure a través del lenguaje de hello R utilizando Hola módulo ejecutar Script de R."
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
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="4dd77-103">Extender el experimento con R</span><span class="sxs-lookup"><span data-stu-id="4dd77-103">Extend your experiment with R</span></span>
<span data-ttu-id="4dd77-104">Puede ampliar la funcionalidad de Hola de estudio de aprendizaje automático de Azure a través del lenguaje de hello R utilizando hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4dd77-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="4dd77-105">Este módulo acepta varios conjuntos de datos de entrada y genera un solo conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="4dd77-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="4dd77-106">Puede escribir un script de R en hello **Script de R** parámetro de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4dd77-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="4dd77-107">Para acceder a cada puerto de entrada del módulo de hello mediante código similar toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="4dd77-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="4dd77-108">Enumeración de todos los paquetes actualmente instalados</span><span class="sxs-lookup"><span data-stu-id="4dd77-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="4dd77-109">puede cambiar la lista de Hola de paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="4dd77-109">hello list of installed packages can change.</span></span> <span data-ttu-id="4dd77-110">Puede encontrar una lista de los paquetes instalados actualmente en [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Paquetes de R compatibles con Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="4dd77-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="4dd77-111">También puede obtener lista de completa y actualizada de Hola de los paquetes instalados escribiendo Hola siguiente código en hello [ejecutar Script de R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="4dd77-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="4dd77-112">Esto envía la lista de hello paquetes toohello de puerto de salida de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4dd77-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="4dd77-113">paquete de hello tooview lista, conecte un módulo de conversión como [convertir tooCSV] [ convert-to-csv] toohello dejado la salida de hello [ejecutar Script de R] [ execute-r-script]módulo, ejecute el experimento de hello, a continuación, haga clic en la salida de hello del módulo de conversión de Hola y seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="4dd77-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Descargar la salida del módulo "Convertir tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="4dd77-115">Importación de paquetes</span><span class="sxs-lookup"><span data-stu-id="4dd77-115">Importing packages</span></span>
<span data-ttu-id="4dd77-116">Puede importar paquetes que no se hayan instalado mediante el uso de hello siguientes comandos de hello [ejecutar Script de R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="4dd77-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="4dd77-117">Hola donde `my_favorite_package.zip` archivo contiene el paquete.</span><span class="sxs-lookup"><span data-stu-id="4dd77-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
