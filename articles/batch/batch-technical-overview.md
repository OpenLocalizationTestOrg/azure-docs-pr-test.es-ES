---
title: "aaaAzure por lotes ejecuta soluciones de computación paralelas a gran escala en nube de hello | Documentos de Microsoft"
description: "Obtenga información acerca de cómo utilizar el servicio de Azure Batch Hola cargas de trabajo HPC y paralelas a gran escala"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Ejecución de cargas de trabajo paralelas intrínsecamente con Batch

Lote de Azure es un servicio de plataforma para ejecutar aplicaciones a gran escala paralelas y de alto rendimiento informática (HPC) eficazmente en la nube de Hola. Lote de Azure programa toorun de trabajo de proceso intensivo en una colección administrada de máquinas virtuales, y puede automáticamente escala calcular necesidades de hello toomeet de recursos de los trabajos.

Con Azure Batch, puede fácilmente definir tooexecute de recursos de proceso de Azure las aplicaciones en paralelo y a escala. No hay ningún toomanually necesidad de crear, configurar y administrar un clúster de HPC, máquinas virtuales individuales, redes virtuales o un trabajo complejo e infraestructura de programación de tareas. Azure Batch automatiza o simplifica estas tareas automáticamente.

## <a name="use-cases-for-batch"></a>Casos de uso de Lote
Batch es un servicio administrado de Azure que se usa para el *procesamiento por lotes* o la *computación por lotes*, es decir, la ejecución de grandes volúmenes de tareas similares para obtener un resultado deseado. La computación por lotes la utilizan normalmente organizaciones que procesan, transforman y analizan grandes volúmenes de datos con regularidad.

Lote funciona bien con cargas de trabajo y aplicaciones intrínsecamente paralelas (a veces llamadas "lamentablemente paralelas"). Las cargas de trabajo intrínsecamente paralelas son las que se dividen fácilmente en varias tareas que trabajan simultáneamente en varios equipos.

![Tareas paralelas][1]<br/>

Algunos ejemplos de cargas de trabajo que normalmente se procesan mediante esta técnica son:

* Modelado de riesgos financieros
* Análisis de datos de clima e hidrología
* Representación, análisis y procesamiento de imágenes
* Codificación y transcodificación multimedia
* Análisis de secuencia genética
* Análisis de esfuerzos en ingeniería
* Pruebas de software

Lote también puede realizar cálculos paralelo con una etapa reduce al final de Hola y ejecutar cargas de trabajo HPC más complejas como [interfaz de paso de mensajes (MPI)](batch-mpi.md) aplicaciones.

Para obtener una comparación entre Lote y otras opciones de solución HPC en Azure, consulte [Soluciones de lote y HPC en la nube de Azure](batch-hpc-solutions.md).

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Escenario: Escalar horizontalmente una carga de trabajo paralela
Una solución común que usa hello las API de lote toointeract con hello servicio por lotes implica la ampliación horizontal de trabajo paralelo intrínsecamente--como representación de Hola de imágenes para escenas 3D: en un grupo de nodos de proceso. Este grupo de nodos de proceso puede ser el "conjunto de representación" que proporciona decenas, cientos o incluso miles de trabajo de procesamiento de tooyour de núcleos, por ejemplo.

Hello siguiente diagrama muestra un flujo de trabajo comunes de lote, con una aplicación cliente o servicio mediante una carga de trabajo paralelo de lote toorun hospedado.

![Flujo de trabajo de soluciones de Lote][2]

En este escenario habitual, la aplicación o servicio procesa una carga de trabajo de cálculo en el lote de Azure mediante la realización de hello pasos:

1. Cargar hello **archivos de entrada** hello y **aplicación** que procesará los tooyour archivos cuenta de almacenamiento de Azure. archivos de entrada de Hello pueden ser cualquier dato que va a procesar la aplicación, como datos de modelado financiero o archivos de vídeo toobe transcodifica. archivos de la aplicación Hello pueden ser cualquier aplicación que se utiliza para procesar datos de hello, como una aplicación de representación 3D o Transcodificador de medios.
2. Crear un lote **grupo** de nodos de cálculo en su cuenta de lote: estos nodos son máquinas virtuales de Hola que va a ejecutar las tareas. Especificar propiedades como hello [tamaño de nodo](../cloud-services/cloud-services-sizes-specs.md), su sistema operativo y la ubicación de hello en el almacenamiento de Azure de hello aplicación tooinstall cuando los nodos de hello unirse a grupo de hello (aplicación de Hola que ha cargado en el paso 1 de #). También puede configurar el grupo de hello[escalar automáticamente](batch-automatic-scaling.md) de carga de trabajo toohello de respuesta que generan las tareas. La escala automática dinámicamente ajusta el número de Hola de nodos de proceso en el grupo de Hola.
3. Crear un lote **trabajo** carga de trabajo de toorun hello en grupo de Hola de nodos de cálculo. Cuando crea un trabajo, lo asocia a un grupo de Lote.
4. Agregar **tareas** toohello trabajo. Cuando se agrega trabajo tooa de tareas, Hola servicio por lotes programa automáticamente las tareas de hello para la ejecución en nodos de proceso de hello en el grupo de Hola. Cada tarea utiliza la aplicación hello que carga los archivos de entrada de hello tooprocess.
   
   * 4a. Antes de que se ejecuta una tarea, pueden descargar datos de hello (archivos de entrada de Hola) que es tooprocess toohello de nodos de proceso que se asigna a. Si aplicación hello no ya se instaló en el nodo de hello (vea el paso 2 de #), se puede descargar aquí en su lugar. Una vez completados Hola descargas, las tareas de Hola se ejecutan en sus nodos asignados.
5. Cuando ejecutan tareas de hello, puede consultar el progreso de Hola de toomonitor de lote de trabajo de Hola y sus tareas. La aplicación de cliente o servicio se comunica con hello servicio por lotes a través de HTTPS. Dado que es posible que esté supervisando miles de tareas que se ejecutan en miles de nodos de proceso, demasiado[consultar el servicio de lote de hello eficazmente](batch-efficient-list-queries.md).
6. Cuando se completan las tareas de hello, puede cargar su tooAzure de datos de resultado almacenamiento. También puede recuperar archivos directamente desde el sistema de archivos de hello en un nodo de proceso.
7. Cuando la supervisión detecta que se han completado las tareas de hello en su trabajo, la aplicación de cliente o servicio puede descargar los datos de salida de hello para su posterior procesamiento o evaluation.

Tenga en cuenta se trata simplemente de una manera toouse por lotes, y este escenario describe sólo algunas de sus características disponibles. Por ejemplo, puede ejecutar [varias tareas en paralelo](batch-parallel-node-tasks.md) en cada nodo de ejecución y puede usar [tareas de preparación y finalización del trabajo](batch-job-prep-release.md) tooprepare Hola nodos para los trabajos, a continuación, limpiar posteriormente.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene una descripción general de hello servicio por lotes, es toolearn un poco más de tiempo toodig cómo puede utilizarlo tooprocess las cargas de trabajo paralelo de proceso intensivo.

* Hola de lectura [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md), información esencial para todo aquel que preparar toouse por lotes. artículo de Hello contiene información más detallada sobre los recursos del servicio por lotes como hello, nodos, trabajos y las tareas y grupos de muchas características de la API que puede usar al compilar la aplicación de lote.
* Obtenga información acerca de hello [herramientas y API de lote](batch-apis-tools.md) disponibles para la creación de soluciones de lote.
* [Empezar a trabajar con la biblioteca de hello Azure Batch para .NET](batch-dotnet-get-started.md) toolearn cómo toouse C# y Hola tooexecute de biblioteca .NET de lotes en una carga de trabajo simple con un flujo de trabajo comunes de lote. En este artículo debe ser uno de su primera detiene mientras aprende cómo toouse Hola servicio por lotes. También hay un [versión de Python](batch-python-tutorial.md) de tutorial Hola.
* Descargar hello [ejemplos en GitHub de código] [ github_samples] toosee cómo C# y Python puedan interactuar con las cargas de trabajo de ejemplo de tooschedule y proceso de lote.
* Extraer del repositorio hello [ruta de acceso de aprendizaje por lotes] [ learning_path] tooget una idea de hello recursos disponibles tooyou que obtenga información acerca de toowork con el lote.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
