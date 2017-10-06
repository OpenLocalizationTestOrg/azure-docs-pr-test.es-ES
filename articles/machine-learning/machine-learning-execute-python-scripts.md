---
title: "máquina de Python aaaExecute secuencias de comandos de aprendizaje | Documentos de Microsoft"
description: "Describe los principios de diseño subyacentes a la compatibilidad con scripts de Python en Aprendizaje automático de Azure y los escenarios de uso básico, las funcionalidades y las limitaciones."
keywords: "aprendizaje automático de Python, pandas, pandas de python, scripts de python, ejecutar scripts de python"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Ejecución de scripts de Python en Aprendizaje automático de Azure | Azure

En este tema se describe los principios de diseño de Hola Hola actual soporte para scripts de Python en aprendizaje automático de Azure subyacente. También se describen funciones principales de Hello proporcionados, incluidos:

- ejecución de escenarios de uso básicos
- puntuación de un experimento en un servicio web
- compatibilidad con la importación de código existente
- exportación de visualizaciones
- selección de características supervisada
- comprensión de algunas limitaciones

[Python](https://www.python.org/) es una herramienta indispensable en pecho de herramienta Hola de muchos de los científicos de datos. Tiene:

* una sintaxis elegante y concisa, 
* asistencia multiplataforma, 
* una amplia colección de bibliotecas eficaces y 
* herramientas de desarrollo perfeccionadas. 

Python se usa en todas las fases de un flujo de trabajo que normalmente se emplea en el modelado de aprendizaje automático:

- ingesta y procesamiento de datos 
- construcción de características
- entrenamiento del modelo 
- validación del modelo
- implementación de modelos de Hola

Azure Machine Learning Studio admite la incrustación de scripts de Python en varias partes de un experimento de aprendizaje automático y, además, su publicación sin problemas como servicios web en Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Principios de diseño de los scripts de Python en Aprendizaje automático

Hola interfaz principal tooPython en estudio de aprendizaje automático de Azure es a través de hello [ejecutar Script de Python] [ execute-python-script] módulo que se muestra en la figura 1.

![imagen1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![imagen2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Figura 1. Hola **ejecutar Script de Python** módulo.

Hola [ejecutar Script de Python] [ execute-python-script] módulo en estudio de aprendizaje automático acepta una toothree entradas y genera una salidas tootwo (descritos en hello siguiente sección), como su analógico R, hello [ Ejecutar Script de R] [ execute-r-script] módulo. Hello toobe de código de Python ejecuta aparece en el cuadro de parámetro hello como un conjunto con nombre especialmente punto de entrada función denominada `azureml_main`. Estos son los principios utilizados tooimplement este módulo de diseño clave hello:

1. *Debe ser idiomático para los usuarios de Python.* La mayoría de los usuarios de Python incluye su código como funciones dentro de módulos. Así, la colocación de muchas instrucciones ejecutables en un módulo de nivel superior es relativamente rara. Como resultado, cuadro de secuencia de comandos de hello también toma una función de Python especialmente con nombre como toojust lugar una secuencia de instrucciones. Hello objetos expuestos en función de hello son tipos de biblioteca de Python estándar como [Pandas](http://pandas.pydata.org/) tramas de datos y [NumPy](http://www.numpy.org/) matrices.
2. *Debe contar con alta fidelidad entre las ejecuciones locales y las ejecuciones en la nube.* Hola Hola tooexecute de back-end utiliza código Python se basa [Anaconda](https://store.continuum.io/cshop/anaconda/), usadas de distribución de Python científico multiplataforma. Se trata con cerrar too200 de paquetes de Python más comunes de Hola. Por lo tanto, los científicos de datos pueden depurar y calificar su código en su entorno Anaconda compatible con la instancia de Azure Machine Learning local. A continuación, usar un entorno de desarrollo existentes, como [IPython](http://ipython.org/) Bloc de notas o [Python Tools para Visual Studio](http://aka.ms/ptvs), toorun como parte de un experimento de aprendizaje automático de Azure. Hola `azureml_main` punto de entrada es una función de Python vainilla de modo que *** pueden crearse sin código específico de aprendizaje automático de Azure u Hola SDK instalado.
3. *Debe admitir composición sin problemas con otros módulos de Aprendizaje automático de Azure.* Hola [ejecutar Script de Python] [ execute-python-script] módulo acepta, como entradas y salidas, conjuntos de datos de aprendizaje automático de Azure estándar. marco subyacente de Hello puentes de forma transparente y eficaz Hola aprendizaje automático de Azure y Python tiempos de ejecución. Por tanto, Python se puede usar con flujos de trabajo existentes de Azure Machine Learning, incluidos los que llaman a R y SQLite. Como resultado, los científicos de datos pueden crear flujos de trabajo que:
   * usen Python y Pandas para el procesamiento previo y la limpieza de datos
   * fuente hello tooa SQL transformación de datos combinar varias características de tooform de conjuntos de datos
   * entrenar modelos utilizando algoritmos de hello en aprendizaje automático de Azure 
   * evaluar y POST-procesar los resultados de hello mediante R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Escenarios de uso básicos de Aprendizaje automático para scripts de Python

En esta sección, se encuesta algunos de los usos básicos de Hola de hello [ejecutar Script de Python] [ execute-python-script] módulo. Módulo de Python toohello entradas se exponen como tramas de datos de Pandas. Hello función debe devolver una trama de datos Pandas única empaquetada dentro de un Python [secuencia](https://docs.python.org/2/c-api/sequence.html) como una tupla, lista o matriz NumPy. a continuación, se devuelve el primer elemento de esta secuencia de Hello en hello primer puerto de salida del módulo de Hola. Este esquema aparece en la figura 2.

![imagen3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Ilustración 2. Asignación de tooparameters de puertos de entrada y puerto toooutput de valor devuelto.

Más semántica de cómo los puertos de entrada de hello obtienen tooparameters asignada de hello `azureml_main` función se muestran en la tabla 1:

![imagen1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabla 1. Asignación de parámetros de toofunction de puertos de entrada.

asignación de Hello entre los puertos de entrada y parámetros de función es posicional:

- puerto de entrada conectados primera Hello es asignada toohello primer parámetro de función hello. 
- Hola segunda entrada (si está conectado) está asignada toohello segundo parámetro de función hello.

Vea *Python para el análisis de datos* (o ' Reilly, 2012) por McKinney Occid. para obtener más información en Pandas de Python y en cómo puede ser usado toomanipulate datos eficiente y eficaz. 


## <a name="translation-of-input-and-output-types"></a>Traslación de tipos de entrada y salida 
Los conjuntos de datos en Azure ML son fotogramas toodata convertido en Pandas. Tramas de datos de salida se convierten en conjuntos de datos de back-tooAzure ML. Hola siguiendo las conversiones se realiza:

1. Las columnas de cadena y numéricos se convierten como-es y valores que faltan en un conjunto de datos son too'NA convertido ' valores en Pandas. Hello misma conversión se realiza en hello hacia atrás (valores de NA de Pandas son toomissing convertido en aprendizaje automático de Azure).
2. Los vectores de índice de Pandas no se admiten en Azure Machine Learning. Todos los marcos de datos de entrada en función de Python de hello siempre tienen un índice numérico de 64 bits desde 0 toohello, número de columnas menos 1. 
3. Los conjuntos de datos de Azure Machine Learning no pueden tener nombres de columnas duplicados ni nombres de columnas que no sean cadenas. Si una trama de datos de salida contiene las columnas no numéricas, Hola llamadas framework `str` en nombres de columna de Hola. De igual modo, los nombres de columna duplicados son tooinsure automáticamente con sufijo Hola nombres son únicos. toohello primer duplicado, toohello segundo duplicado (3) y así sucesivamente, se agrega el sufijo de Hello (2).


## <a name="operationalizing-python-scripts"></a>Funcionamiento de los scripts de Python

Cuando un experimento de puntuación se publica como servicio web, se llama a todos los módulos [Ejecutar script de Python][execute-python-script] usados en él. Por ejemplo, en la figura 3 se muestra un experimento de puntuación que contiene código de hello tooevaluate una única expresión de Python. 

![imagen4](./media/machine-learning-execute-python-scripts/figure3a.png)

![imagen5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Figura 3. Servicio web para evaluar una expresión de Python.

Un servicio web creado a partir de este experimento:

- toma como entrada una expresión de Python (como una cadena)
- envía toohello intérprete de Python 
- Devuelve una tabla que contiene la expresión de Hola y el resultado de hello evaluada.


## <a name="importing-existing-python-script-modules"></a>Importación de módulos existentes de scripts de Python

Un caso de uso común para muchas científicos de datos es tooincorporate scripts existentes de Python en experimentos de aprendizaje automático de Azure. En lugar de requerir que todo el código se concatenarán y pegar en el cuadro de una única secuencia de comandos, Hola [ejecutar Script de Python] [ execute-python-script] módulo acepta un archivo zip que contiene los módulos de Python en el puerto de entrada tercer Hola. se descomprimió el archivo Hello por marco de trabajo de ejecución de hello en tiempo de ejecución y contenido de Hola se agrega la ruta de acceso de biblioteca de toohello de intérprete de Python Hola. Hola `azureml_main` función, a continuación, puede importar estos módulos directamente el punto de entrada.

Por ejemplo, considere la posibilidad de archivo hello Hello.py que contiene una función simple "Hola, mundo".

![imagen6](./media/machine-learning-execute-python-scripts/figure4.png)

Figura 4. Función definida por el usuario en el archivo Hello.py.

A continuación, creamos un archivo Hello.zip que contiene Hello.py:

![imagen7](./media/machine-learning-execute-python-scripts/figure5.png)

Figura 5. Archivo ZIP que contiene código Python definido por el usuario.

Cargue el archivo zip de hello como un conjunto de datos en estudio de aprendizaje automático de Azure. A continuación, crear y ejecutar un experimento con código de Python de hello en el archivo de hello Hello.zip adjuntando toohello tercer puerto de entrada de hello **ejecutar Script de Python** módulo, como se muestra en esta ilustración.

![imagen8](./media/machine-learning-execute-python-scripts/figure6a.png)

![imagen9](./media/machine-learning-execute-python-scripts/figure6b.png)

Figura 6. Experimento de ejemplo con código Python definido por el usuario cargado como archivo ZIP.

salida del módulo hello muestra el archivo zip Hola ha estado desempaquetar y esa función hello `print_hello` se ha ejecutado.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Figura 7. Función definida por el usuario en uso dentro de hello [ejecutar Script de Python] [ execute-python-script] módulo.


## <a name="working-with-visualizations"></a>Trabajo con visualizaciones

Pueden devolver trazados creadas con MatplotLib que se puede visualizar en el Explorador de Hola Hola [ejecutar Script de Python][execute-python-script]. Pero Hola gráficos no están tooimages redirigido automáticamente como si estuvieran cuando se usa R. Por lo que el usuario Hola debe guardarlos explícitamente de los trazados tooPNG archivos si están toobe devuelve tooAzure atrás aprendizaje automático. 

imágenes de toogenerate desde MatplotLib, debe completar Hola siguiendo el procedimiento:

* cambiar Hola back-end demasiado "AGG" de hello predeterminado basado en Qt representador 
* cree un nuevo objeto de figura, 
* obtener el eje de Hola y generar todos los gráficos en él 
* Guardar archivo de hello figura tooa PNG 

Este proceso se muestra en hello después de la figura 8 que crea una matriz de gráfico de dispersión en función de hello scatter_matrix Pandas.

![imagen1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Figura 8. El código toosave que matplotlib cifras tooimages.

Ilustración 9 se muestra un experimento con script de Hola que se ha mostrado anteriormente tooreturn traza a través de hello segundo puerto de salida.

![imagen2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![imagen2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Figura 9. Visualización de los gráficos generados a partir del código Python.

Es posible tooreturn varias figuras guardándolas en diferentes imágenes, Hola aprendizaje automático de Azure en tiempo de ejecución recoge todas las imágenes y concatena para visualización.


## <a name="advanced-examples"></a>Ejemplos avanzados

entorno Anaconda Hola está instalado en aprendizaje automático de Azure contiene paquetes comunes como NumPy, SciPy y Scikits-Learn. Estos paquetes se pueden usar de forma efectiva para distintas tareas de procesamiento de datos en una canalización de aprendizaje automático. Por ejemplo, hello script y experimento siguiente ilustran Hola uso de aprendices de conjunto de puntuaciones de importancia de características de toocompute Scikits-Learn para un conjunto de datos. puntuaciones de Hello pueden ser usado tooperform supervisado de selección de características antes de pasarlas a otro modelo de aprendizaje automático.

Este es puntuaciones de importancia de hello Python función usa toocompute hello y características de hello orden según las puntuaciones de hello:

![imagen11](./media/machine-learning-execute-python-scripts/figure8.png)

Figura 10. Función toorank características puntuaciones.
 Hello experimento siguiente, a continuación, calcula y devuelve las puntuaciones de importancia de Hola de características Hola "Pima Índico Diabetes" conjunto de datos de aprendizaje automático de Azure:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Figura 11. Características de toorank de experimento en el conjunto de datos de hello Pima Índico Diabetes.

## <a name="limitations"></a>Limitaciones
Hola [ejecutar Script de Python] [ execute-python-script] tiene actualmente Hola siguientes limitaciones:

1. *Ejecución en espacio aislado.* en tiempo de ejecución de Python de Hello es actualmente en un espacio aislado y, como resultado, no permitir que el sistema de archivos local de red o toohello de toohello de acceso de forma persistente. Todos los archivos guardados localmente se aislado y se eliminan cuando finaliza el módulo de Hola. Hola código Python no tiene acceso a la mayoría de los directorios en la máquina de Hola que se ejecuta en, hello las excepciones son Hola directorio actual y sus subdirectorios.
2. *Falta de compatibilidad con la depuración y desarrollo sofisticado.* módulo de Python Hola actualmente no admite las características del IDE como intellisense y la depuración. Además, si se produce un error en el módulo de hello en tiempo de ejecución, hello seguimiento de pila de Python completa está disponible. Pero debe verse en el registro de salida de hello para el módulo de Hola. Actualmente, se recomienda desarrollar y depurar scripts de Python en un entorno como IPython y, a continuación, importar el código de hello en el módulo de Hola.
3. *Salida de una trama de datos.* punto de entrada de Python de Hello es solo permitido tooreturn una trama de datos único como salida. No es posible actualmente tooreturn que Python arbitrario objetos como modelos entrenados directamente realizar copias en tiempo de ejecución de toohello aprendizaje automático de Azure. Al igual que [ejecutar Script de R][execute-r-script], que tiene Hola misma limitación, es posible en muchos casos toopickle objetos en un byte de matriz y, a continuación, devuelven que dentro de una trama de datos.
4. *Incapacidad toocustomize instalación de Python*. Actualmente, hello solo forma tooadd Python módulos personalizados es a través del mecanismo de archivos zip Hola se ha descrito anteriormente. A pesar de que esto es viable cuando se trata de módulos pequeños, es complicado para módulos de gran tamaño (especialmente para los módulos con DLL nativas) o para un gran número de módulos. 

## <a name="conclusions"></a>Conclusiones
Hola [ejecutar Script de Python] [ execute-python-script] módulo permite científico de datos código Python existente de tooincorporate en flujos de trabajo de aprendizaje de máquina hospedada en la nube en aprendizaje automático de Azure y tooseamlessly incorporación de operatividad a ellas como parte de un servicio web. módulo de script de Python Hola naturalmente interopera con otros módulos de aprendizaje automático de Azure. Hola módulo puede utilizarse para una variedad de tareas de procesamiento de datos exploración toopre y extracción de características y, a continuación, tooevaluation y posteriores al procesamiento de resultados de Hola. en tiempo de ejecución de un back-end Hola utilizado para la ejecución se basa en Anaconda, una distribución de Python probada y ampliamente utilizada. Este back-end facilita automáticamente los activos de código existentes tooon panel en la nube de Hola.

Esperamos que tooprovide funcionalidad adicional toohello [ejecutar Script de Python] [ execute-python-script] módulo como Hola tootrain de capacidad y hacer operativos los modelos de Python y tooadd mejor compatibilidad para Hola desarrollo y depuración de código en estudio de aprendizaje automático de Azure.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
