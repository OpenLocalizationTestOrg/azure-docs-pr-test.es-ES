---
title: "aaaALM aprendizaje automático de Azure | Documentos de Microsoft"
description: "Aplicar procedimientos recomendados de administración del ciclo de vida de las aplicaciones en Azure Machine Learning Studio"
keywords: "ALM, AML, Azure ML, administración del ciclo de vida de las aplicaciones, control de versiones"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Administración del ciclo de vida de las aplicaciones en Azure Machine Learning Studio
Estudio de aprendizaje automático de Azure es una herramienta para desarrollar los experimentos de aprendizaje automático que son operaciones en la plataforma de nube de Azure Hola. Es como Hola IDE de Visual Studio y servicio de nube escalables que se combinan en una sola plataforma. Puede incorporar las prácticas estándar de Application Lifecycle Management (ALM), de control de versiones distintos la implementación y ejecución de tooautomated de activos en estudio de aprendizaje automático de Azure. En este artículo se describe algunos de los enfoques y las opciones de Hola.

## <a name="versioning-experiment"></a>Control de versiones del experimento
Hay dos tooversion maneras recomendadas sus experimentos. Puede confiar en el historial de ejecución integrado, o exportar experimento hello en formato JavaScript Object Notation (JSON) y administrarlo de externamente. Cada enfoque tiene sus ventajas e inconvenientes.

### <a name="experiment-snapshots-using-run-history"></a>Instantáneas del experimento mediante el historial de ejecución
En el modelo de ejecución de Hola de hello experimento de aprendizaje de estudio de aprendizaje automático de Azure, cada vez que haga clic en hello **ejecutar** botón en el editor de experimento de hello, una instantánea inmutable del experimento de hello es programador de trabajos de toohello enviado. Puede ver esta lista de instantáneas, haga clic en hello **historial de ejecución de** botón de barra de comandos de hello en la vista de editor de hello experimento.

![Botón Historial de ejecución](media/machine-learning-version-control/runhistory.png)

Se puede, a continuación, instantánea Hola abierto en modo bloqueado haciendo clic en nombre de hello del experimento de hello en el experimento de hello tiempo Hola fue enviado toorun y se tomó la instantánea de Hola. Tenga en cuenta que solo Hola primer elemento de lista de hello, que representa el experimento de hello actual, está en un estado Editable. Tenga en cuenta además que cada instantánea puede tener también diversos estados, incluidos completado (ejecución parcial), de error, de error (ejecución parcial) o de borrador.

![Lista del historial de ejecuciones](media/machine-learning-version-control/runhistorylist.png)

Después de que ha abierto, puede guardar Hola instantánea experimento como un experimento de nuevo y, a continuación, modificarlo. Si la instantánea de experimento contiene activos como un modelo entrenado, la transformación y el conjunto de datos que se han actualizado las versiones, instantánea Hola conserva la versión original de hello referencias toohello cuando se tomó la instantánea de Hola. Si guarda Hola bloqueado instantánea como un experimento de nuevo, estudio de aprendizaje automático de Azure detecta la existencia de Hola de una versión más reciente de estos activos y automáticamente se actualiza en el experimento nueva Hola.

Si elimina el experimento de hello, se eliminan todas las instantáneas de ese experimento.

### <a name="exportimport-experiment-in-json-format"></a>Exportar o importar experimento en formato JSON
las instantáneas del historial de Hello ejecutar conservar una versión inmutable del experimento de hello en estudio de aprendizaje automático de Azure cada vez que se hayan enviado toorun. Puede guardar una copia local del experimento de Hola y protegerlo de sistema de control de origen favoritos tooyour, como Team Foundation Server y volver a crear más adelante en un experimento desde ese archivo local. Puede usar hello [PowerShell de Azure Machine Learning](http://aka.ms/amlps) cmdlets [ *AmlExperimentGraph de exportación* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) y [  *Importar AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish que.

archivo JSON de Hello es una representación textual de hello experimentar gráfico, lo que puede incluir un tooassets de referencia en el área de trabajo de Hola como un conjunto de datos o un modelo entrenado. No contiene una versión serializada de activos de Hola. Si intentas documento JSON de tooimport hello en el área de trabajo de hello, activos de hello al que hace referencia ya deben existir con hello mismo asset identificadores que se hace referencia en el experimento de Hola. En caso contrario, no será capaz de tooaccess Hola importado experimento.

## <a name="versioning-trained-model"></a>Control de versiones de un modelo entrenado
Un modelo entrenado en aprendizaje automático de Azure se serializa en un formato conocido como un archivo .iLearner y se almacena en la cuenta de almacenamiento de blobs de Azure Hola asociada con el área de trabajo de Hola. Una manera de tooget una copia del archivo de .iLearner Hola es a través de hello reciclaje API. [En este artículo](machine-learning-retrain-models-programmatically.md) explica cómo funciona el Hola reciclaje API. pasos de alto nivel de Hello:

1. Actualice el experimento de entrenamiento.
2. Agregar un módulo de Hola que genera Hola entrenado, como optimizar Hyperparameter de modelo o crear modelo R o módulo entrenar modelo de toohello de puerto de salida de web service.
3. Ejecute el experimento de entrenamiento y, a continuación, impleméntelo como servicio web de entrenamiento de modelos.
4. Llamada Hola extremo BES del servicio web de aprendizaje de Hola y especifique el nombre de archivo de hello .iLearner deseado y ubicación de la cuenta de almacenamiento Blob donde se almacenará.
5. Finaliza la cosecha Hola generado .iLearner archivo después de llamar Hola BES.

Archivo de otra manera tooretrieve hello .iLearner es a través de hello PowerShell commandlet [ *descarga AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Esto podría ser más fácil si solo desea tooget una copia de hello .iLearner archivo sin modelo de hello necesidad tooretrain hello mediante programación.

Después de obtener hello .iLearner archivo que contiene el modelo entrenado hello, a continuación, puede emplear su propia estrategia de control de versiones. Hola estrategia puede ser tan simple como aplicar un pre/sufijo como una convención de nomenclatura y simplemente dejando archivo .iLearner de hello en almacenamiento de blobs o copiar/importación en el sistema de control de versiones.

archivo de guardado .iLearner Hello, a continuación, puede utilizarse para puntuar a través de servicios web implementados.

## <a name="versioning-web-service"></a>Control de versiones de un servicio web
Puede implementar dos tipos de servicios web a partir de un experimento de Azure Machine Learning. servicio web clásico de Hello está asociado estrechamente al experimento hello, así como el área de trabajo de Hola. nuevo servicio web de Hello usa el marco de trabajo de hello Azure Resource Manager, y ya no está unida experimento original de Hola o área de trabajo de Hola.

### <a name="classic-web-service"></a>Servicio web clásico
tooversion un servicio web clásico, puede sacar partido de construcción de punto de conexión de servicio de hello web. Este es un flujo típico:

1. A partir de su experimento predictivo, implementa un nuevo servicio web clásico, que contiene un punto de conexión predeterminado.
2. Crear un nuevo extremo denominado ep2, que expone la versión actual de Hola de hello experimento/entrenar modelo.
3. Vuelve y actualiza el experimento predictivo y el modelo entrenado.
4. Volver a implementar experimento predictivo hello, que, a continuación, actualizará el punto de conexión de hello predeterminado. Sin embargo, esto no modificará ep2.
5. Crear un punto de conexión adicional denominada ep3, que expone la nueva versión de hello del experimento de Hola y el modelo entrenado.
6. Practique toostep 3 si es necesario.

Con el tiempo, es posible que tenga muchos puntos de conexión creados en hello mismo servicio web. Cada punto de conexión representa una copia en el momento del experimento de Hola que contiene Hola puntual en versión de modelo entrenado Hola. A continuación, puede usar toodetermine lógica externa que toocall de punto de conexión, lo que equivale a seleccionar una versión del programa Hola a entrena el modelo de ejecución de la puntuación de Hola.

También puede crear muchos extremos del servicio web idénticos y, a continuación, aplicar revisiones distintas versiones de hello .iLearner archivo toohello extremo tooachieve efecto similar a. [En este artículo](machine-learning-create-models-and-endpoints-with-powershell.md) explica con más detalle cómo tooaccomplish que.

### <a name="new-web-service"></a>Servicio web nuevo
Si crea un nuevo servicio web basado en Azure Resource Manager, la construcción de punto de conexión de Hola ya no está disponible. En su lugar, puede generar archivos de definición (WSD) del servicio web, en formato JSON, su experimento predicción mediante el uso de hello [AmlWebServiceDefinitionFromExperiment de exportación](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) commandlet de PowerShell, o mediante el uso de hello [ *Exportación AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) commandlet de PowerShell desde un servicio web basado en el Administrador de recursos implementados.

Una vez haya exportado de hello versión y el archivo WSD controlan, también puede implementar Hola WSD como un nuevo servicio web en un plan de servicio web diferente en una región distinta de Azure. Asegúrese de que proporcionar cuenta de almacenamiento adecuado de hello configuración, así como hello web nuevo Id. del plan de servicio. toopatch en archivos .iLearner diferente, puede modificar el archivo WSD de hello y referencia de la ubicación de actualización Hola de hello entrenado modelo e implementarlo como un nuevo servicio web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatizar la ejecución e implementación del experimento
Un aspecto importante de ALM es toobe tooautomate capaz de Hola la ejecución y proceso de implementación de aplicación hello. Aprendizaje automático de Azure, puede hacerlo mediante el uso de hello [módulo de PowerShell](http://aka.ms/amlps). Este es un ejemplo-to-end de pasos de proceso de implementación/ejecución tooa relevante estándar ALM automatizada mediante el uso de hello [módulo de PowerShell de Azure Machine Learning Studio](http://aka.ms/amlps). Cada paso está vinculado tooone o más cmdlets de PowerShell que puede usar tooaccomplish ese paso.

1. [Cargue un conjunto de datos](https://github.com/hning86/azuremlps#upload-amldataset).
2. Copie un experimento de entrenamiento en el área de trabajo de Hola desde una [área de trabajo](https://github.com/hning86/azuremlps#copy-amlexperiment) o de [galería](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), o [importar](https://github.com/hning86/azuremlps#import-amlexperimentgraph) una [exportar](https://github.com/hning86/azuremlps#export-amlexperimentgraph) experimentar desde disco local.
3. [Actualizar el conjunto de datos de hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) en el experimento de entrenamiento de Hola.
4. [Ejecute el experimento de entrenamiento de hello](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Promover entrenado hello](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Copiar un experimento predictivo](https://github.com/hning86/azuremlps#copy-amlexperiment) en el área de trabajo de Hola.
7. [Modelo entrenado de actualización hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) en experimento predictivo Hola.
8. [Ejecutar el experimento de predicción de hello](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Implementar un servicio web](https://github.com/hning86/azuremlps#new-amlwebservice) de experimento predictivo Hola.
10. Probar el servicio web de hello [RR](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) o [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) punto de conexión.

## <a name="next-steps"></a>Pasos siguientes
* Descargar hello [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) tooautomate módulo e iniciar las tareas ALM.
* Obtenga información acerca de cómo demasiado[crear y administrar gran número de modelos de aprendizaje automático mediante un experimento de único](machine-learning-create-models-and-endpoints-with-powershell.md) a través de PowerShell y API de reciclaje.
* Obtenga más información sobre cómo [implementar los servicios web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
