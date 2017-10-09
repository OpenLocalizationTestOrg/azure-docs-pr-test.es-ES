---
title: "módulo de aaaPowerShell para el aprendizaje automático | Documentos de Microsoft"
description: "módulo de PowerShell de Hello para el aprendizaje automático de Azure está disponible en modo de vista previa pública. Usar PowerShell toocreate y administrar áreas de trabajo, experimentos, servicios web y mucho más."
keywords: "experimento,regresión lineal,algoritmos de aprendizaje automático,tutorial de aprendizaje automático,técnicas de modelado predictivo,experimento de ciencia de datos"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Módulo de PowerShell para Aprendizaje automático de Microsoft Azure
módulo de PowerShell de Hello para el aprendizaje automático de Azure es una herramienta eficaz que le permite áreas de trabajo de toouse Windows PowerShell toomanage, experimentos, conjuntos de datos, los servicios web estándar y más.

Puede ver la documentación de Hola y descargar el módulo de hello, junto con el código fuente completo de hello, en [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> módulo de PowerShell de Azure Machine Learning Hola está actualmente en modo de vista previa. módulo de Hello continuará toobe mejorado y ampliado durante este período de vista previa. Esté atento hello [Cortana Intelligence y Blog de aprendizaje automático](https://blogs.technet.microsoft.com/machinelearning/) de noticias y obtener información.

## <a name="what-is-hello-machine-learning-powershell-module"></a>¿Qué es el módulo de PowerShell de aprendizaje de máquina de hello?
módulo de PowerShell de aprendizaje de máquina de Hello una. Módulo DLL basada en red que permite toofully Administrar áreas de trabajo de aprendizaje automático de Azure, experimentos, conjuntos de datos, servicios web de clásico y extremos del servicio web clásico de Windows PowerShell. 

Junto con el módulo de hello, puede descargar el código fuente completo Hola que incluye un limpiamente separados [capa de API de C#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). Esto significa que puede hacer referencia a este archivo DLL desde su propio proyecto .NET y administrar Azure Machine Learning por medio de código. NET. Además, Hola DLL depende de las API de REST subyacente que puede usar directamente desde el cliente de favoritos.

## <a name="what-can-i-do-with-hello-powershell-module"></a>¿Qué puedo hacer con el módulo de PowerShell de hello?
Estas son algunas de las tareas de Hola que puede realizar con este módulo de PowerShell. Extraer del repositorio hello [completa documentación](https://aka.ms/amlps) para éstos y muchas más funciones.

* Aprovisionar una nueva área de trabajo mediante un certificado de administración ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Exportar e importar un archivo JSON que representa un gráfico de experimento ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Ejecutar un experimento ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Crear un servicio web a partir de un experimento de predicción ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Crear un punto de conexión en un servicio web publicado ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Invocar un punto de conexión de servicio web RRS o BES ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) e [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Este es un ejemplo rápido de usar PowerShell toorun un experimento existente:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Para un caso de uso más detallado, consulte el artículo sobre el uso de tooautomate de módulo de PowerShell de hello una tarea más solicitados: [crear extremos de servicio de muchos modelos de aprendizaje automático y web de un experimento con PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>¿Cómo empiezo?
tooget a trabajar con PowerShell de aprendizaje de máquina, descargue hello [paquete de versión](https://github.com/hning86/azuremlps/releases) de GitHub y seguir hello [instrucciones para la instalación](https://github.com/hning86/azuremlps/blob/master/README.md). instrucciones de Hello explican cómo toounblock Hola descargado y había descomprimido DLL y, a continuación, importación en el entorno de PowerShell. La mayoría de hello cmdlets requieren que se proporcione el identificador de área de trabajo de hello, token de autorización del área de trabajo de hello y Hola región de Azure que Hola área de trabajo está en. valores de hello de manera más sencillos de Hello tooprovide es a través de un archivo de config.json predeterminado. instrucciones de Hello también explican cómo tooconfigure este archivo. 

Y si lo desea, puede clonar el árbol de git de hello, modificar el código de hello y compilar localmente mediante Visual Studio.

## <a name="next-steps"></a>Pasos siguientes
Puede encontrar documentación completa de hello para el módulo de PowerShell de hello en [https://aka.ms/amlps](https://aka.ms/amlps). 

Para obtener un ejemplo completo sobre cómo toouse Hola módulo en un escenario real, desprotección Hola detallada caso de uso, [crear extremos de servicio de muchos modelos de aprendizaje automático y web de un experimento con PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
