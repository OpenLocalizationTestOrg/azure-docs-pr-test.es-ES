---
title: "datos de aaaImport en estudio de aprendizaje automático | Documentos de Microsoft"
description: "¿Cómo tooimport los datos en estudio de aprendizaje automático de Azure desde varios orígenes de datos. Obtenga información sobre qué tipos de datos y formatos de datos son compatibles."
keywords: "importar datos, formato de datos, tipos de datos, orígenes de datos, datos de entrenamiento"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importación de datos de entrenamiento en Estudio de aprendizaje automático de Azure desde varios orígenes de datos
toouse sus propios datos en estudio de aprendizaje automático toodevelop y entrenar una solución de análisis predictivos, puede: 

* cargar datos desde una **archivo local** de tiempo de la unidad de disco duro toocreate un módulo de conjunto de datos en el área de trabajo
* acceso a datos de uno de varios **orígenes de datos en línea** mientras está ejecutando el experimento usando hello [importar datos] [ import-data] módulo 
* Usar datos de otro **experimento** de Azure Machine Learning guardado como un conjunto de datos.
* Usar los datos de instancia local de **SQL Server Database**.

Cada una de estas opciones se describe en uno de los temas de hello en el menú de Hola a continuación. Estos temas muestra cómo toouse en estudio de aprendizaje automático de los orígenes de datos de tooimport de estos datos distintos. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Existe una gran variedad de conjuntos de datos de ejemplo disponibles en Machine Learning Studio que puede usar como datos de aprendizaje. Para obtener información al respecto, consulte [usar conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático de Azure](machine-learning-use-sample-datasets.md)).
> 
> 

Este tema de Introducción también describe cómo tooget datos listos para usar en estudio de aprendizaje automático y se admiten los tipos de datos y formatos de datos. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Preparación de los datos para usarlos en Estudio de aprendizaje automático de Azure
Estudio de aprendizaje automático es toowork diseñada con datos rectangulares o tabulares, como datos de texto que se delimitan o estructura de una base de datos, aunque en algunas circunstancias se pueden usar datos no rectangulares.

Se recomienda que los datos estén relativamente limpios. Es decir, le interesará tootake atención problemas tales como las cadenas sin comillas antes de cargar datos de hello en el experimento.

Sin embargo, hay módulos disponibles en Estudio de aprendizaje automáticos que le permitirán manipular levemente los datos en el experimento. Dependiendo de los algoritmos de aprendizaje automático de Hola que vamos a usar, puede que necesite toodecide cómo podrá controlar problemas estructurales de datos como los valores que faltan y datos dispersos, y hay módulos que pueden ayudar a que. Buscar en hello **transformación de datos** sección de la paleta de módulo de Hola para módulos que llevan a cabo estas funciones.

Puede ver o descargar datos Hola generado por un módulo haciendo clic en el puerto de salida de hello en cualquier momento en el experimento. Función de módulo de hello, puede haber descarga diferentes opciones disponibles o es posible que los datos de hello toovisualize pueda dentro del explorador web en estudio de aprendizaje automático.

## <a name="data-formats-and-data-types-supported"></a>Tipos y formatos de datos admitidos
Puede importar un número de tipos de datos en el experimento, dependiendo de qué mecanismo use datos tooimport y donde procede de:

* Texto sin formato (.txt)
* Valores separados por coma (CSV) con un encabezado (.csv) o sin encabezado (.nh.csv)
* Valores separados con tabulaciones (TSV) con un encabezado (.tsv) o sin encabezado (.nh.tsv)
* Archivo de Excel
* Tabla de Azure
* Tabla de Hive
* Tabla de Base de datos SQL
* Valores de OData
* Datos de SVMLight (.svmlight) (vea hello [SVMLight definición](http://svmlight.joachims.org/) para obtener información de formato)
* Atributo de datos de formato de archivo de relación (ARFF) (.arff) (vea hello [definición ARFF](http://weka.wikispaces.com/ARFF) para obtener información de formato)
* Archivo ZIP (.zip)
* Archivo de área de trabajo u objeto de R (.RData)

Si importa los datos en un formato como ARFF que incluya los metadatos, estudio de aprendizaje automático utiliza este encabezado de metadatos toodefine Hola y el tipo de datos de cada columna.

Si importa los datos como formato TSV o CSV que no incluya estos metadatos, estudio de aprendizaje automático deduce el tipo de datos de Hola para cada columna mediante el muestreo de datos de Hola. Si los datos de hello también no tienen encabezados de columna, estudio de aprendizaje automático proporciona nombres predeterminados.

Puede especificar explícitamente o cambiar Hola encabezados y tipos de datos para las columnas con hello [editar metadatos][edit-metadata].

siguiente Hello **tipos de datos** reconocidos por estudio de aprendizaje automático:

* String
* Entero
* Doble
* Booleano
* DateTime
* TimeSpan

Estudio de aprendizaje automático utiliza un tipo de datos interno denominado ***tabla de datos*** datos toopass entre módulos. Puede convertir explícitamente los datos en formato de tabla de datos mediante hello [convertir tooDataset] [ convert-to-dataset] módulo.

Cualquier módulo que acepta formatos distintos de la tabla de datos, Hola datos tooData tabla se convertirá en modo silencioso antes de pasarlo toohello siguiente módulo.

En caso de ser necesario, puede convertir el formato Tabla de datos de vuelta al formato CSV, TSV, ARFF o SVMLight mediante el uso de otros módulos de conversión.
Buscar en hello **conversiones de formato de datos** sección de la paleta de módulo de Hola para módulos que llevan a cabo estas funciones.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
