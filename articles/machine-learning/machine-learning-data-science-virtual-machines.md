---
title: "Datos de máquinas virtuales Azure ciencia como servidores de Bloc de notas de IPython aaaProvision | Documentos de Microsoft"
description: "Configuración de una máquina virtual de ciencia de datos como un IPython Notebook Server con herramientas compatibles."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Aprovisionamiento de máquinas de virtuales de ciencia de datos de Azure como IPython Notebook Servers
Las instrucciones están siempre aquí que describen cómo tooset una VM de Azure y una máquina virtual de Azure con el servicio de SQL como servidores de Bloc de notas de IPython. máquina virtual de Windows Hello se configura con compatibilidad con herramientas como Bloc de notas de IPython, Explorador de almacenamiento de Azure y AzCopy, así como otras utilidades que son útiles para los proyectos de ciencia de datos. Explorador de almacenamiento de Azure y AzCopy, por ejemplo, proporcionan a modos cómodos tooupload datos tooAzure almacenamiento desde su equipo local o toodownload se tooyour el equipo local desde el almacenamiento. 

Este menú vincula tootopics que describen cómo tooset seguridad Hola varios entornos de ciencia de datos utilizan hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Varios tipos de máquinas virtuales de Azure se pueden aprovisionar y configurar toobe usa como parte de un entorno de ciencia de datos en la nube. Decisión de Hello sobre qué tipo de máquina virtual toouse depende del tipo hello y la cantidad de datos toobe se modela con aprendizaje automático y el destino de Hola para esos datos en la nube de Hola. 

* Para obtener instrucciones sobre Hola preguntas tooconsider al tomar esta decisión, vea [Plan Your Azure máquina aprendizaje datos ciencia Environment](machine-learning-data-science-plan-your-environment.md). 
* Para un catálogo de algunos de los escenarios de Hola que puede surgir al realizar el análisis avanzado, consulte [Hola de escenarios para el proceso de análisis avanzado y tecnología de aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md)

Se proporcionan dos conjuntos de instrucciones:

* [Configurar una máquina virtual de Azure como un servidor de Bloc de notas de IPython para análisis avanzado](machine-learning-data-science-setup-virtual-machine.md) muestra cómo tooprovision una máquina virtual de Azure con el Bloc de notas de IPython y otras herramientas usa toodo ciencia de datos para los casos en que una forma de almacenamiento de Azure que no sea de SQL puede ser usado toostore Hola datos.
* [Configurar una máquina virtual de Azure SQL Server como un servidor de Bloc de notas de IPython para análisis avanzado](machine-learning-data-science-setup-sql-server-virtual-machine.md) muestra cómo tooprovision una máquina virtual de Azure SQL Server con el Bloc de notas de IPython y otras herramientas usa toodo ciencia de datos para los casos en que una base de datos SQL puede ser usado toostore Hola datos.

Una vez que aprovisionados y configurados, estas máquinas virtuales está listos para su uso como servidores de Bloc de notas de IPython de exploración de Hola y el procesamiento de datos y para otras tareas necesarias junto con aprendizaje automático de Azure y Hola proceso de ciencia de datos de equipo (TDSP). pasos siguientes en el proceso de ciencia de datos Hola Hola se asignan una Hola [ruta de acceso de aprendizaje de TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir los pasos que se mueven datos en SQL Server o HDInsight, procesar y ejemplo allí como preparación para el aprendizaje a partir de los datos de hello con Azure Aprendizaje automático.

> [!NOTE]
> Las máquinas virtuales de Azure tienen unas tarifas del tipo **pague solo por lo que use**. tooensure que no están siendo factura cuando no se utiliza la máquina virtual, tiene toobe en hello **detenido (desasignado)** estado de hello [Portal clásico de Azure](http://manage.windowsazure.com/). Para obtener instrucciones paso a paso o cómo toodeallocate máquina virtual, consulte [apagado y cancelar la asignación de la máquina virtual cuando no esté en uso](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

