---
title: "aaaClean y preparar los datos para aprendizaje automático de Azure | Documentos de Microsoft"
description: "Tooprepare de procesamiento previo y limpiar los datos para aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Datos de tooprepare de tareas para el aprendizaje automático mejorada
El preprocesamiento y la limpieza de datos son tareas importantes que normalmente se deben llevar a cabo para que el conjunto de datos se pueda usar de forma eficaz para el aprendizaje automático. Los datos sin procesar son a menudo ruidosos no confiables y es posible que les falten valores. El uso de estos datos para el modelado puede producir resultados engañosos. Estas tareas forman parte de hello proceso de ciencia de datos de equipo (TDSP) y normalmente siguen una exploración inicial de un toodiscover de conjunto de datos usado y el procesamiento previo de plan Hola necesario. Para obtener instrucciones sobre el proceso de hello TDSP más detallada, consulte los pasos de hello descritos en hello [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Procesamiento previo y tareas de limpieza, como tarea de exploración de datos de hello, puede llevarse a cabo en una amplia variedad de entornos, como SQL o subárbol o estudio de aprendizaje automático de Azure y con diversas herramientas y lenguajes, como R o Python, donde los datos están en función de almacena y cómo se da formato. Puesto que TDSP es iterativa por naturaleza, estas tareas pueden tener lugar en varios pasos de flujo de trabajo de hello del proceso de Hola.

Este artículo presenta varios conceptos de procesamiento de datos y tareas que se pueden llevar a cabo antes o después de introducir datos en Aprendizaje automático de Azure.

Para obtener un ejemplo de exploración de datos y procesamiento previo realizado dentro de estudio de aprendizaje automático de Azure, vea hello [procesar previamente los datos en estudio de aprendizaje automático de Azure](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) vídeo.

## <a name="why-pre-process-and-clean-data"></a>¿Por qué preprocesar y limpiar datos?
Recopilar los datos del mundo real de varios orígenes y procesos y pueden contener irregularidades o poner en peligro la calidad de hello del conjunto de datos de Hola de datos dañados. problemas de calidad de datos típico de Hola que surgen son:

* **Incompletos**: en los datos no hay atributos o contienen valores que faltan.
* **Ruidosos**: los datos contienen registros erróneos o valores atípicos.
* **Incoherentes**: los datos contienen discrepancias o registros en conflicto.

Los datos de calidad son un requisito previo para los modelos predictivos de calidad. tooavoid "elementos no utilizados de elementos no utilizados out" y mejorar la calidad de datos y, por tanto, el rendimiento de modelo, es imperativo tooconduct un toospot de pantalla de mantenimiento de datos, datos emite al principio y decidir Hola correspondiente de procesamiento de datos y pasos de limpieza.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>¿Cuáles son algunas pantallas de mantenimiento de datos más habituales que se emplean?
Podemos comprobar Hola general de calidad de datos mediante la comprobación:

* Hola número de **registros**.
* Hola número de **atributos** (o **características**).
* atributo de Hello **tipos de datos** (nominal, ordinal o continuo).
* Hola número de **valores que faltan**.
* **Corrección** de datos de Hola.
  * Si los datos de hello en TSV o CSV, compruebe que los separadores de columna de Hola y separadores de línea siempre correctamente separarán líneas y columnas.
  * Si los datos de hello están en formato HTML o XML, compruebe si los datos de hello están bien formados basándose en sus respectivos estándares.
  * Analizar también puede ser necesario en la información del pedido tooextract estructurada de datos estructurados o semiestructurados.
* **Registros de datos incoherentes**. Se permiten comprobación Hola intervalo de valores. Por ejemplo, si los datos de hello contienen GPA estudiante, compruebe si está Hola GPA Hola designado intervalo, diga 0 ~ 4.

Cuando se detectan problemas con los datos, **pasos de procesamiento** es necesario que a menudo consiste en limpiar los valores que faltan, normalización de datos, la discretización, tooremove de procesamiento de texto o reemplazar caracteres incrustados que pueden afectar a alineación de datos, mixtos tipos de datos en común campos y otros.

**El aprendizaje automático de Azure consume datos tabulares con formato correcto**.  Si los datos de hello ya están en formato tabular, preprocesamiento de datos puede realizarse directamente con aprendizaje automático de Azure en hello estudio de aprendizaje automático.  Si los datos no están en formato tabular, se encuentra en el análisis de XML, por ejemplo puede ser necesario en formulario de pedido tooconvert Hola datos tootabular.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>¿Cuáles son algunas de las principales tareas de hello en el procesamiento previo de datos?
* **Limpieza de datos**: rellene los valores que faltan, detecte y quite los valores atípicos y los datos con ruido.
* **Transformación de datos**: normalizar las dimensiones de tooreduce de datos y ruido.
* **Reducción de datos**: atributos o registros de datos de ejemplo para un control de datos más sencillo.
* **Discretización de datos**: Convert continua atributos toocategorical atributos para facilitar su uso con ciertos métodos de aprendizaje automático.
* **Limpieza de texto**: quite caracteres incrustados que puedan ocasionar errores en la alineación de los datos, por ejemplo, pestañas incrustadas en un archivo de datos separado por tabulaciones, nuevas líneas incrustadas que pueden dividirse en registros, etc.

Hola las siguientes secciones detallan algunos de estos pasos de procesamiento de datos.

## <a name="how-toodeal-with-missing-values"></a>¿La valoración toodeal con la que falta?
toodeal con valores que faltan, es mejor toofirst identificar el motivo de Hola de hello falta valores problema de toobetter identificador hello. Los métodos de control de valores que faltan típicos son:

* **Eliminación**: quite los registros con los valores que faltan
* **Sustitución ficticia**: reemplace los valores que faltan por un valor ficticio; por ejemplo, *desconocido* para categorías o 0 para valores numéricos.
* **Significa sustitución**: si los datos que faltan hello están numéricos, reemplazar valores que faltan Hola por la media de Hola.
* **Sustitución más frecuentes**: si los datos que faltan hello están de categorías, reemplazar valores que faltan Hola por elemento más frecuente de Hola
* **Sustitución de regresión**: utilice una falta de regresión método tooreplace los valores que tienen valores devueltas.  

## <a name="how-toonormalize-data"></a>¿Cómo toonormalize datos?
Tooa de valores numéricos de volver a escala de normalización de datos especifica el intervalo. Entre los métodos de normalización de datos más conocidos se incluyen:

* **Normalización mínimo-máximo**: transformar el rango de hello datos tooa, por ejemplo entre 0 y 1, donde hello el valor mínimo es too0 escalado y el valor máximo too1 linealmente.
* **Normalización de puntuación-z**: escalar en función de la media y desviación estándar de datos: dividir diferenciar hello en datos de Hola y Hola Media por la desviación estándar de Hola.
* **Ajuste de escala en decimal**: escalar datos Hola móvil Hola separador decimal del valor de atributo de Hola.  

## <a name="how-toodiscretize-data"></a>¿Cómo toodiscretize datos?
Pueden ser de datos discretos datos mediante la conversión de atributos de valores continuos toonominal o intervalos. Algunas formas de hacerlo son las siguientes:

* **Discretización de igual ancho**: dividir intervalo Hola de todos los valores posibles de un atributo en grupos de N de hello mismo tamaño y asignar valores de hello que se encuentran en una ubicación con el número de bin Hola.
* **Discretización de la misma altura**: dividir el intervalo de Hola de todos los valores posibles de un atributo en grupos de N, cada uno con Hola mismo número de instancias, a continuación, asignar Hola valores que se encuentran en una ubicación con hello cubo número.  

## <a name="how-tooreduce-data"></a>¿Cómo tooreduce datos?
Hay varios métodos tooreduce tamaño de los datos para el control de datos sea más fáciles. Función de dominio de hello y tamaño de los datos, se puede aplicar Hola siguientes métodos:

* **Grabar muestreo**: registros de datos de Hola de ejemplo y elija solo subconjunto representativo de hello en datos Hola.
* **Atributo muestreo**: seleccionar solo un subconjunto de los atributos más importantes de Hola de datos de Hola.  
* **Agregación**: dividir los datos de hello en grupos y almacenar los números de Hola para cada grupo. Por ejemplo, hello ingresos diarios pueden ser números de una cadena de restaurante sobre Hola últimos 20 años agregan tamaño de hello tooreduce toomonthly los ingresos de los datos de Hola.  

## <a name="how-tooclean-text-data"></a>¿Cómo tooclean los datos de texto?
**campos de texto en datos tabulares** pueden incluir caracteres que afectan a los límites de registros o alineación de columnas. Por ejemplo, las pestañas incrustadas en un archivo separado por tabulaciones causan un error de alineación de columnas y los caracteres de nueva línea incrustados dividen las líneas de registro. Control al texto de lectura/escritura de codificación de texto incorrecto da lugar a pérdida de tooinformation, involuntario introducción de caracteres no se puede leer, por ejemplo, valores NULL, y puede también afectan al texto de análisis. Pueden ser necesario analizar cuidado y Editar orden tooclean en campos de texto para la correcta alineación o datos tooextract estructurada de datos de texto no estructurados o semiestructurados.

**Exploración de datos** ofrece una vista temprana en datos Hola. Una serie de problemas de datos puede ser han cubierto durante este paso y métodos correspondientes pueden ser tooaddress aplicado esos problemas.  Es importante tooask preguntas como ¿qué es Hola origen del problema de Hola y cómo problema Hola puede haberse producido. Esto también ayuda a decidir en los pasos de procesamiento de datos de Hola que toobe necesidad realizada tooresolve ellos. tipo de Hola de visión uno tiene intención de tooderive de datos de hello también puede ser esfuerzo de procesamiento de datos de hello tooprioritize usado.

## <a name="references"></a>Referencias
> *_Minería de datos: conceptos y técnicas*, Tercera edición, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber y Jian Pei
> 
> 

