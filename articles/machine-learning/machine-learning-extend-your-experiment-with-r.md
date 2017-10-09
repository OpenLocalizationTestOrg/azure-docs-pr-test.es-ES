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
# <a name="extend-your-experiment-with-r"></a>Extender el experimento con R
Puede ampliar la funcionalidad de Hola de estudio de aprendizaje automático de Azure a través del lenguaje de hello R utilizando hello [ejecutar Script de R] [ execute-r-script] módulo.

Este módulo acepta varios conjuntos de datos de entrada y genera un solo conjunto de datos como salida. Puede escribir un script de R en hello **Script de R** parámetro de hello [ejecutar Script de R] [ execute-r-script] módulo.

Para acceder a cada puerto de entrada del módulo de hello mediante código similar toohello siguiente:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Enumeración de todos los paquetes actualmente instalados
puede cambiar la lista de Hola de paquetes instalados. Puede encontrar una lista de los paquetes instalados actualmente en [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Paquetes de R compatibles con Azure Machine Learning).

También puede obtener lista de completa y actualizada de Hola de los paquetes instalados escribiendo Hola siguiente código en hello [ejecutar Script de R] [ execute-r-script] módulo:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Esto envía la lista de hello paquetes toohello de puerto de salida de hello [ejecutar Script de R] [ execute-r-script] módulo.
paquete de hello tooview lista, conecte un módulo de conversión como [convertir tooCSV] [ convert-to-csv] toohello dejado la salida de hello [ejecutar Script de R] [ execute-r-script]módulo, ejecute el experimento de hello, a continuación, haga clic en la salida de hello del módulo de conversión de Hola y seleccione **descargar**. 

![Descargar la salida del módulo "Convertir tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importación de paquetes
Puede importar paquetes que no se hayan instalado mediante el uso de hello siguientes comandos de hello [ejecutar Script de R] [ execute-r-script] módulo:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

Hola donde `my_favorite_package.zip` archivo contiene el paquete.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
