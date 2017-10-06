---
title: "escenarios de aaaIdentify y planear el proceso de análisis - Azure | Documentos de Microsoft"
description: "Plan para análisis avanzado teniendo en cuenta una serie de cuestiones claves."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Cómo tooidentify escenarios y planear avanzado procesamiento de datos de análisis
¿Qué recursos debe tiene pensado tooinclude al configurar un entorno toodo avanzada análisis de procesamiento en un conjunto de datos? Este artículo sugiere una serie de tooask de preguntas que le ayudará a identificar las tareas de Hola y proporcionar los recursos necesarios en su escenario. se indica el orden de Hola de pasos de alto nivel para realizar análisis predictivos en [¿qué es hello proceso de ciencia de datos de equipo (TDSP)?](data-science-process-overview.md). Cada uno de estos pasos requerirá recursos específicos para el escenario concreto de hello tareas tooyour relevante. Hola tooidentify preguntas clave su escenario preocupación datos logística, características, calidad de Hola de conjuntos de datos de hello y herramientas de Hola y lenguajes prefiere analysis de hello toodo.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Cuestiones de logística: movimiento y ubicaciones de los datos
preguntas logística Hola conciernen a la ubicación de Hola de hello **origen de datos**, hello **destino** en Azure y los requisitos para mover datos de hello, incluidos los recursos, la cantidad y la programación de Hola implicados. datos de Hola que necesite toobe mueve varias veces durante el proceso de análisis de Hola. Un escenario común es toomove de datos locales en alguna forma de almacenamiento en Azure y, a continuación, en estudio de aprendizaje automático.

1. **¿Cuál es el origen de datos?** ¿Es local o en la nube de hello? Por ejemplo:
   
   * datos de Hello están disponibles públicamente en una dirección HTTP.
   * datos de Hello residen en una ubicación de archivos de red o local.
   * datos de Hello están en una base de datos de SQL Server.
   * Hola datos se almacenan en un contenedor de almacenamiento de Azure
2. **¿Qué es hello Azure destino?** ¿Dónde necesita toobe para el procesamiento o modelado? Por ejemplo:
   
   * Almacenamiento de blobs de Azure
   * Bases de datos SQL Azure
   * SQL Server en máquinas virtuales de Azure
   * HDInsight (Hadoop en Azure) o tablas de Hive
   * Aprendizaje automático de Azure
   * Discos duros virtuales de Azure que se pueden montar.
3. **¿Cómo va datos de hello toomove?**  Hola procedimientos y los recursos disponibles tooingest o cargar datos en una serie de almacenamiento diferente y entornos de procesamiento se describen en los temas siguientes de Hola.
   
   * [Carga de datos en entornos de almacenamiento para el análisis](machine-learning-data-science-ingest-data.md)
   * [Importación de datos de entrenamiento en Azure Machine Learning Studio desde varios orígenes de datos](machine-learning-data-science-import-data.md)
4. **¿Necesita datos hello toobe movido según una programación regular o modificadas durante la migración?** Considere el uso de factoría de datos de Azure (ADF) cuando continuamente migra datos necesidades toobe, especialmente si un escenario híbrido que tenga acceso tanto de forma local y recursos de nube está implicado, o cuando se lleva a cabo datos Hola o necesita toobe modificado o tienen lógica de negocios Agregar tooit en curso de Hola de que se está migrando. Para obtener más información, consulte [mover datos desde un servidor SQL local tooSQL Azure con Data Factory de Azure](machine-learning-data-science-move-sql-azure-adf.md)
5. **¿La cantidad de datos de hello es tooAzure toobe mover?** Conjuntos de datos que sean muy grandes pueden superar la capacidad de determinados entornos de almacenamiento de Hola. Para obtener un ejemplo, vea la explicación de Hola de límites de tamaño de estudio de aprendizaje automático en la sección siguiente Hola. En tales casos, un ejemplo de Hola datos puede utilizarse durante el análisis de Hola. Para obtener información detallada de cómo toodown muestra un conjunto de datos en varios entornos de Azure, consulte [datos Hola proceso de ciencia de datos de equipo de ejemplo](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Cuestiones sobre las características de los datos: tipo, formato y tamaño
Estas preguntas es tooplanning clave el almacenamiento y procesamiento de entornos, cada uno de los cuales están toovarious adecuado tipos de datos y cada uno de los cuales tienen ciertas restricciones.

1. **¿Qué tipos de datos de hello?** Por ejemplo:
   
   * Numérico
   * Categorías
   * Cadenas
   * Binary
2. **¿Qué formato tienen los datos?** Por ejemplo:
   
   * Archivos sin formato separados por comas (CSV) o separados por tabulaciones (TSV)
   * Comprimidos o sin comprimir
   * Blobs de Azure
   * Tablas de Hadoop Hive
   * Tablas de SQL Server
3. **¿Qué tamaño tienen los datos?**
   
   * Pequeño: menos de 2 GB
   * Medio: más de 2 GB y menos de 10 GB
   * Grande: más de 10 GB

Tomemos como ejemplo el entorno de estudio de aprendizaje automático de Azure de hello:

* Para obtener una lista de formatos de datos de Hola y tipos admitidos por estudio de aprendizaje automático de Azure, consulte [formatos de datos y los tipos de datos compatibles](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) sección.
* Para obtener información sobre las limitaciones de datos de estudio de aprendizaje automático de Azure, vea hello **lo grande puede Hola ser conjunto de datos para mi módulos?** sección de [importar y exportar datos para el aprendizaje automático](machine-learning-faq.md#machine-learning-studio-questions)

Para obtener información sobre las limitaciones de Hola de otros servicios de Azure que se usa en el proceso de análisis de hello, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Cuestiones sobre la calidad de los datos: exploración y procesamiento previo
1. **¿Qué sabe acerca de los datos?** Explorar los datos cuando necesite toogain un comprender sus características básicas. ¿Qué patrones o tendencias muestran, qué valores atípicos tienen o cuántos valores faltan? Este paso es importante para determinar el alcance de Hola de procesamiento previo necesario, para la formulación de hipótesis que podrían sugerir características más adecuadas de Hola o tipo de análisis y para la formulación de planes de recopilación de datos adicionales. Calcular estadísticas descriptivas y trazar visualizaciones son técnicas útiles para la inspección de datos. Para obtener información detallada de cómo tooexplore un conjunto de datos en varios entornos de Azure, consulte [explorar datos en hello proceso de ciencia de datos de equipo](machine-learning-data-science-explore-data.md).
2. **¿Datos de hello requiere procesamiento previo o limpieza?**
   El preprocesamiento y la limpieza de datos son tareas importantes que normalmente se deben llevar a cabo para que el conjunto de datos se pueda usar de forma eficaz para el aprendizaje automático. Los datos sin procesar son a menudo ruidosos no confiables y es posible que les falten valores. El uso de estos datos para el modelado puede producir resultados engañosos. Para obtener una descripción, consulte [tooprepare datos para el aprendizaje automático mejorada de tareas](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Cuestiones sobre herramientas y lenguajes
Hay muchas opciones dependiendo de qué lenguajes y entornos de desarrollo o herramientas necesita o prefiere usar.

1. **¿Qué idiomas hacer prefiere toouse para el análisis?**  
   
   * R
   * Python
   * SQL
2. **¿Qué herramientas debe usar para analizar los datos?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -un lenguaje de script utiliza tooadminister los recursos de Azure en un lenguaje de script.
   * [Estudio de aprendizaje automático de Azure](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools para Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Jupyter Notebooks](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Identificación del escenario de análisis avanzado
Una vez que haya respondido a las preguntas de hello en la sección anterior de hello, está listo toodetermine qué escenario que mejor se adapte a su caso. se describen escenarios de ejemplo de Hola en [escenarios para análisis avanzado en aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md).

