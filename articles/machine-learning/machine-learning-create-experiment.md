---
title: "aaaA experimento sencillo en estudio de aprendizaje automático | Documentos de Microsoft"
description: "Este tutorial de aprendizaje automático le guiará a través de un sencillo experimento de ciencia de datos. Se podrá predecir precio Hola de un automóvil con un algoritmo de regresión."
keywords: "experimento,regresión lineal,algoritmos de aprendizaje automático,tutorial de aprendizaje automático,técnicas de modelado predictivo,experimento de ciencia de datos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Tutorial de aprendizaje automático: creación del primer experimento de ciencia de datos en Estudio de aprendizaje automático de Azure

Si nunca ha usado **Azure Machine Learning Studio** antes, este tutorial le ayudará.

En este tutorial, le mostraremos cómo toouse Studio para hello es la primera vez toocreate un experimento de aprendizaje automático. el experimento de Hello probará un modelo analítico que predice el precio de Hola de un automóvil en función de diferentes variables como marca y especificaciones técnicas.

> [!NOTE]
> Este tutorial muestra conceptos básicos de Hola de módulos de cómo toodrag y colocar en el experimento, conéctelos, ejecutar el experimento de Hola y examine los resultados de Hola. No entraremos toodiscuss Hola tema general de aprendizaje automático o cómo tooselect y uso Hola 100 + datos y algoritmos manipulación módulos integrados incluidos en Studio.
>
>Si es nuevo aprendizaje toomachine, Hola serie de vídeos [ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) podría ser un buen lugar toostart. Esta serie de vídeos es un aprendizaje de toomachine introducción excelente con conceptos y lenguaje cotidiano.
>
>Si está familiarizado con el aprendizaje automático, pero desea obtener información más general sobre estudio de aprendizaje automático y contiene los algoritmos de aprendizaje de automático de hello, aquí tiene algunos recursos buena:
>
- [¿Qué es Estudio de aprendizaje automático?](machine-learning-what-is-ml-studio.md) - Esta es una descripción de alto nivel de Studio.
- [Aspectos básicos con ejemplos de algoritmo de aprendizaje máquina](machine-learning-basics-infographic-with-algorithm-examples.md) -este infografía es útil si desea más información acerca de los distintos tipos de algoritmos de aprendizaje automático incluidos con estudio de aprendizaje automático de hello toolearn.
- [Guía de aprendizaje de máquina](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -esta guía ofrece información similar como hello infografía anterior, pero en un formato interactivo.
- [Equipos de hoja de referencia de algoritmo de aprendizaje](machine-learning-algorithm-cheat-sheet.md) y [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md) -este póster descargable y artículo complementario describe los algoritmos de Studio hello en profundidad.
- [Estudio de aprendizaje automático: Algoritmo y ayuda del módulo](https://msdn.microsoft.com/library/azure/dn905974.aspx) -se trata de referencia completa de Hola para todos los módulos de estudio, incluidos los algoritmos de aprendizaje automático,

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>¿Cómo funciona la ayuda de Estudio de aprendizaje automático?

Estudio de aprendizaje automático resulta fácil tooset seguridad un experimento con módulos de arrastrar y colocar preprogramados con las técnicas de modelado de predicción.

Mediante un área de trabajo visual e interactiva, se arrastran y colocan ***conjuntos de datos*** y ***módulos*** de análisis en un lienzo interactivo. Conéctelos tooform junto un ***experimentar*** que se ejecutan en estudio de aprendizaje automático.
Se ***crear un modelo de***, ***entrenar el modelo de hello***, y ***puntuación y prueba Hola modelo***.

En el diseño del modelo, puede iterar edición experimento de Hola y ejecutarlo hasta que se proporciona Hola resultados que está buscando. Cuando el modelo está listo, puede publicarlo como un ***servicio web*** para que otros puedan enviarle nuevos datos y obtener a cambio predicciones.

## <a name="open-machine-learning-studio"></a>Apertura de Machine Learning Studio

tooget trabajar con Studio, vaya demasiado[https://studio.azureml.net](https://studio.azureml.net). Si ya se ha registrado en Machine Learning Studio antes, haga clic en **Sign In** (Iniciar sesión). De lo contrario, haga clic en **Sign up here** (Regístrese aquí) y elija entre opciones gratuitas y de pago.

![Inicie sesión en estudio de aprendizaje tooMachine][sign-in-to-studio]
<br/>
***Inicie sesión en estudio de aprendizaje tooMachine***

## <a name="five-steps-toocreate-an-experiment"></a>Cinco pasos toocreate un experimento

En este tutorial de aprendizaje de máquina, podrá seguir cinco pasos básicos toobuild un experimento en estudio de aprendizaje automático toocreate, entrenar y puntuación el modelo:

- **Crear un modelo**
    - [Paso 1: Obtener los datos]
    - [Paso 2: Preparar los datos de Hola]
    - [Paso 3: Definir las características]
- **Entrenar el modelo de Hola**
    - [Paso 4: Elegir y aplicar un algoritmo de aprendizaje]
- **Modelo de Hola de puntuación y prueba**
    - [Paso 5: Predecir los precios de los automóviles nuevos]

[Paso 1: Obtener los datos]: #step-1-get-data
[Paso 2: Preparar los datos de Hola]: #step-2-prepare-the-data
[Paso 3: Definir las características]: #step-3-define-features
[Paso 4: Elegir y aplicar un algoritmo de aprendizaje]: #step-4-choose-and-apply-a-learning-algorithm
[Paso 5: Predecir los precios de los automóviles nuevos]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Puede encontrar una copia de trabajo de hello siguientes experimento en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com). Vaya demasiado**[la ciencia de datos primer experimentar - predicción de precios de automóviles](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  y haga clic en **abierta en Studio** toodownload una copia del experimento de hello en el aprendizaje automático Área de trabajo de Studio.


## <a name="step-1-get-data"></a>Paso 1: Obtener los datos

Hola primera cosa que necesita el aprendizaje automático de tooperform es datos.
Machine Learning Studio incluye varios conjuntos de datos que puede usar; otra opción es importarlos de diversos orígenes. En este ejemplo, vamos a usar el conjunto de datos de ejemplo de Hola, **datos de precios de automóviles (Raw)**, que se incluye en el área de trabajo.
Este conjunto de datos incluye entradas para diversos automóviles individuales, por ejemplo, información sobre la marca, el modelo, las especificaciones técnicas y el precio.

Le mostramos cómo tooget Hola conjunto de datos en el experimento.

1. Cree un experimento de nuevo haciendo clic en **+ nuevo** en hello parte inferior de la ventana de estudio de aprendizaje automático de hello, seleccione **experimentar**y, a continuación, seleccione **experimentar en blanco**.

2. el experimento de Hello recibe un nombre predeterminado que puede ver en parte superior de hello del lienzo de Hola. Seleccione este texto y cambie su nombre toosomething significativo, por ejemplo, **predicción de precios de automóviles**. nombre de Hello no necesita toobe único.

    ![Cambiar el nombre de experimento Hola][rename-experiment]

2. toohello izquierda del lienzo del experimento de hello es una paleta de conjuntos de datos y los módulos. Tipo de **automobile** en el cuadro de búsqueda de hello en la parte superior de Hola de este conjunto de datos Hola del toofind de paleta con la etiqueta **datos de precios de automóviles (Raw)**. Arrastre este lienzo del experimento toohello conjunto de datos.

    ![Buscar Hola automóviles dataset y arrástrelo al lienzo del experimento de Hola][type-automobile]
    <br/>
    ***Buscar Hola automóviles dataset y arrástrelo al lienzo del experimento de Hola***

toosee lo que estos datos parece, haga clic en el puerto de salida de hello en parte inferior de hello del conjunto de datos de automóviles de hello y, a continuación, seleccione **visualizar**.

![Haga clic en el puerto de salida de hello y seleccione "Visualizar"][select-visualize]
<br/>
***Haga clic en el puerto de salida de hello y seleccione "Visualizar"***

> [!TIP]
> Conjuntos de datos y los módulos con entrada y puertos de salida representados por círculos pequeños - puertos de entrada en la parte superior de hello, salida puertos en la parte inferior de Hola.
toocreate un flujo de datos a través de su experimento, se conectará un puerto de salida del puerto de entrada de tooan de un módulo de otro.
En cualquier momento, puede hacer clic en puerto de salida de hello de un conjunto de datos o un módulo toosee qué datos hello es similar en ese momento en el flujo de datos de Hola.

En este conjunto de datos de ejemplo, cada instancia de un automóvil aparece como una fila y variables de hello asociadas a cada automóvil aparecen como columnas. Proporcionan las variables de Hola para un objeto automobile específico, vamos precio de hello tootry toopredict en la columna derecha (columna 26, titulada "price").

![Ver los datos de automóviles hello en la ventana de visualización de datos de hello][visualize-auto-data]
<br/>
***Ver los datos de automóviles hello en la ventana de visualización de datos de hello***

Ventana de visualización de hello cerrar haciendo clic en hello "**x**" en la esquina superior derecha de Hola.

## <a name="step-2-prepare-hello-data"></a>Paso 2: Preparar los datos de Hola

Normalmente, un conjunto de datos requiere algún procesamiento previo antes de que se pueda analizar. Por ejemplo, puede que haya observado Hola los valores presentes en las columnas de Hola de varias filas que faltan. Estos valores que faltan necesitan toobe limpiarse, así que el modelo de hello puede analizar datos de hello correctamente. En nuestro caso, quitaremos todas las filas que tengan valores ausentes. Además, Hola **pérdidas normalizadas** columna tiene una gran proporción de valores que faltan, por lo que se podrá excluir esa columna de modelo de Hola por completo.

> [!TIP]
> Hola limpiadora no tiene los valores de datos de entrada es un requisito previo para usar la mayoría de módulos de Hola.

En primer lugar agregamos un módulo que quita hello **pérdidas normalizadas** columna completamente, y, a continuación, agregamos otro módulo que quita cualquier fila que tenga los datos que faltan.

1. Tipo de **seleccionar columnas** en cuadro de búsqueda de hello en parte superior de Hola Hola de hello módulo paleta toofind [seleccionar columnas de conjunto de datos] [ select-columns] módulo, a continuación, arrastre el lienzo del experimento toohello . Este módulo permite tooselect qué columnas de datos se desea tooinclude o excluir de Hola modelo.

2. Conecte los puertos de salida de hello de hello **datos de precios de automóviles (Raw)** toohello de conjunto de datos de entrada de puerto de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

    ![Agregar Hola "Seleccionar columnas de conjunto de datos" módulo toohello experimento lienzo y conéctelo][type-select-columns]
    <br/>
    ***Agregar Hola "Seleccionar columnas de conjunto de datos" módulo toohello experimento lienzo y conéctelo***

3. Haga clic en hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y haga clic en **selector de columna de inicio** en hello **propiedades** panel.

    - Hola izquierda, haga clic en **con reglas**
    - En **Empiezan por**, haga clic en **Todas las columnas**. Esto indica [seleccionar columnas de conjunto de datos] [ select-columns] toopass a través de todas las columnas de hello (excepto las columnas que estamos sobre tooexclude).
    - Seleccionar en listas desplegables hello **excluir** y **nombres de columna**y, a continuación, haga clic en el cuadro de texto de Hola. A continuación, se mostrará una lista de columnas. Seleccione **pérdidas normalizadas**, y es agregado toohello cuadro de texto.
    - Haga clic en el selector de columnas de hello tooclose botón de marca de verificación (Aceptar) hello (en Hola inferior derecha).

    ![Iniciar el selector de columna de Hola y excluir Hola "pérdidas normalizadas" columna][launch-column-selector]
    <br/>
    ***Iniciar el selector de columna de Hola y excluir Hola "pérdidas normalizadas" columna***

    Panel de propiedades de hello ahora de **seleccionar columnas de conjunto de datos** indica que pasará a través de todas las columnas de conjunto de datos de hello excepto **pérdidas normalizadas**.

    ![panel de propiedades de Hello muestra que se excluye esa columna Hola "pérdidas normalizadas"][showing-excluded-column]
    <br/>
    ***panel de propiedades de Hello muestra que se excluye esa columna Hola "pérdidas normalizadas"***

    > [!TIP]
    Puede agregar un módulo tooa comentario haciendo doble clic en módulo de Hola y de escritura de texto. Esto puede ayudarle a ver de un vistazo qué módulo Hola está haciendo en el experimento. En este caso, haga doble clic en hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y tipo Hola comentario "Exclude normaliza las pérdidas".
    >
    >


    ![Haga doble clic en un tooadd módulo un comentario][add-comment]
    <br/>
    ***Haga doble clic en un tooadd módulo un comentario***

3. Hola arrastre [limpiar datos que faltan] [ clean-missing-data] toohello módulo experimentar lienzo y conéctelo toohello [seleccionar columnas de conjunto de datos] [ select-columns] módulo. Hola **propiedades** panel, seleccione **quitar toda la fila** en **modo de limpieza**. Esto indica [limpiar datos que faltan] [ clean-missing-data] tooclean datos de hello mediante la eliminación de filas que tienen valores que faltan. Haga doble clic en el módulo de Hola y escriba el comentario de Hola "Quitar filas que faltan de valor".

    ![Establecer el modo de limpieza Hola demasiado "quitar toda la fila" para el módulo de "Limpiar datos que faltan" hello][set-remove-entire-row]
    <br/>
    ***Establecer el modo de limpieza Hola demasiado "quitar toda la fila" para el módulo de "Limpiar datos que faltan" hello***

4. Ejecute el experimento de hello haciendo clic en **ejecutar** final Hola de página Hola.

    Cuando el experimento de hello ha terminado de ejecutarse, todos los módulos de hello tienen un tooindicate de marca de verificación verde que finalizó correctamente. Tenga en cuenta también Hola **finalice la ejecución** estado en la esquina superior derecha de Hola.

![Después de ejecutarlo, experimento Hola debe tener un aspecto similar al siguiente][early-experiment-run]
<br/>
***Después de ejecutarlo, experimento Hola debe tener un aspecto similar al siguiente***

> [!TIP]
> ¿Por qué se se ejecutó experimento Hola ahora? Ejecución experimento hello, pasan las definiciones de columna de Hola para nuestros datos de conjunto de datos de hello, a través de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y a través de hello [limpiar datos que faltan] [ clean-missing-data] módulo. Esto significa que los módulos que nos conectamos demasiado[limpiar datos que faltan] [ clean-missing-data] también tendrá la misma información.

Todo lo que hemos realizado en el experimento de hello toothis punto es datos Hola limpia. Si desea que el conjunto de datos de tooview Hola limpiado, haga clic en hello dejado el puerto de salida de hello [limpiar datos que faltan] [ clean-missing-data] módulo y seleccione **visualizar**. Tenga en cuenta que hello **pérdidas normalizadas** ya no se incluye la columna, y no falta ningún valor.

Ahora que los datos de hello están limpios, estamos toospecify listo las características que se vayan a toouse en el modelo de predicción de Hola.

## <a name="step-3-define-features"></a>Paso 3: Definir las características

En el aprendizaje automático, las *características* son propiedades mensurables individuales de algo que le interesa. En nuestro conjunto de datos, cada fila representa un automóvil y cada columna es una característica de ese automóvil.

Buscar un buen conjunto de características para crear un modelo de predicción requiere experimentación y conocimientos sobre el problema de Hola que desea toosolve. Algunas características son mejores para predecir el destino de Hola que otros. Además, algunas características tienen una correlación fuerte con otras y se pueden quitar. Por ejemplo, mpg ciudad y autopista mpg están estrechamente relacionados por lo que podemos conservar uno y quitar Hola otro sin afectar sustancialmente a predicción Hola.

Vamos a crear un modelo que utiliza un subconjunto de características de hello en el conjunto de datos. Puede volver a verle y seleccionar diversas características, vuelva a ejecutar el experimento de Hola y vea si se pueden obtener mejores resultados. Pero toostart, probemos Hola siguientes características:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Arrastre otra [seleccionar columnas de conjunto de datos] [ select-columns] toohello módulo experimentar lienzo. Conectar Hola dejado el puerto de salida de hello [limpiar datos que faltan] [ clean-missing-data] entrada toohello de módulo de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

    ![Conectar Hola "Seleccionar columnas de conjunto de datos" toohello "Limpiar datos que faltan" módulo][connect-clean-to-select]
    <br/>
    ***Conectar Hola "Seleccionar columnas de conjunto de datos" toohello "Limpiar datos que faltan" módulo***

2. Haga doble clic en el módulo de Hola y escriba "Seleccionar características para la predicción."

2. Haga clic en **selector de columna de inicio** en hello **propiedades** panel.

3. Haga clic en **With rules**(Con reglas).

4. En **Empezar por**, haga clic en **No columns** (Ninguna columna). En la fila de filtro de hello, seleccione **Include** y **nombres de columna** y seleccione la lista de nombres de columna en el cuadro de texto de Hola. Esto indica Hola módulo toonot paso a través de las columnas (funciones), salvo que especificamos Hola.

5. Haga clic en el botón de marca de verificación (Aceptar) Hola.

    ![Seleccione tooinclude de columnas (funciones) de hello en la predicción de Hola][select-columns-to-include]
    <br/>
    ***Seleccione tooinclude de columnas (funciones) de hello en la predicción de Hola***

Esto genera un conjunto de datos filtrado que contiene características de hello solo que queremos toohello toopass vamos a usar en el paso siguiente Hola de algoritmo de aprendizaje. Posteriormente puede volver e intentarlo de nuevo con una selección diferente de características.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Paso 4: Elegir y aplicar un algoritmo de aprendizaje

Ahora que los datos de hello están listos, generar un modelo predictivo consta de entrenamiento y prueba. Vamos a usar nuestro modelo de datos tootrain hello y, a continuación, lo probaremos Hola modelo toosee cercanía es toopredict capaz de precios.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*Clasificación* y *regresión* son dos tipos de algoritmos de aprendizaje automático supervisado. La clasificación permite predecir una respuesta a partir de un conjunto definido de categorías, como el color (rojo, azul o verde). La regresión es toopredict usa un número.

Dado que deseamos toopredict precio, que es un número, vamos a usar un algoritmo de regresión. En este ejemplo, vamos a usar un sencillo modelo de *regresión lineal*.

> [!TIP]
> Si desea más información acerca de los distintos tipos de algoritmos de aprendizaje automático toolearn y cuando toouse usarlas, podría ver vídeo primera Hola Hola ciencia de datos para la serie de principiantes, [Hola cinco preguntas respuestas de ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). También puede mirar hello infografía [máquina aspectos básicos con ejemplos de algoritmo de aprendizaje](machine-learning-basics-infographic-with-algorithm-examples.md), o extraer del repositorio hello [máquina hoja de referencia de algoritmo de aprendizaje](machine-learning-algorithm-cheat-sheet.md).

Se entrenar el modelo de hello proporcionando un conjunto de datos que incluye el precio de Hola. modelo de Hello examina datos hello y buscar correlaciones entre las características de un automóvil y su precio. A continuación, se probará el modelo de hello: comenzaremos proporcionan un conjunto de características para automóviles con que estamos familiarizados y ver cómo cerrar modelo Hola procede precio conocido de toopredicting Hola.

Vamos a usar nuestros datos para entrenar el modelo de Hola y probarla mediante la división de datos de hello en conjuntos de datos de prueba y entrenamiento de independiente.

1. Seleccione y arrastre hello [dividir datos] [ split] toohello módulo experimentar lienzo y conéctelo toohello última [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

2. Haga clic en hello [dividir datos] [ split] tooselect de módulo se. Buscar hello **fracción de filas de hello en primer lugar de conjunto de datos de salida** (Hola **propiedades** toohello del panel derecho del lienzo de hello) y lo ha configurado too0.75. De esta manera, se podrá usar 75 por ciento hello tootrain Hola del modelo de datos y retener 25 por ciento para pruebas (más adelante, puede experimentar con diferentes porcentajes de uso).

    ![Hola conjunto dividir fracción de Hola "Dividir datos" módulo too0.75][set-split-data-percentage]
    <br/>
    ***Hola conjunto dividir fracción de Hola "Dividir datos" módulo too0.75***

    > [!TIP]
    > Cambiando hello **valor de inicialización aleatorio** parámetro, puede generar diferentes muestras para entrenar y probar de manera aleatoria. Este parámetro controla Hola la propagación de generador de números seudoaleatorios Hola.

2. Ejecute el experimento de Hola. Cuando se ejecuta el experimento de hello, Hola [seleccionar columnas de conjunto de datos] [ select-columns] y [dividir datos] [ split] módulos pasan toohello de definiciones de columna módulos que iremos agregando a continuación.  

3. Hola tooselect algoritmo de aprendizaje expanda hello **de aprendizaje automático** categoría en hello módulo paleta toohello izquierda de hello lienzo y, a continuación, expanda **inicializar modelo**. Esto muestra varias categorías de módulos que pueden ser algoritmos de aprendizaje automático de tooinitialize usado. Para este experimento, seleccione hello [regresión lineal] [ linear-regression] módulo en hello **regresión** categoría y arrástrelo toohello lienzo del experimento.
(Se puede encontrar el módulo de hello escribiendo "regresión lineal" en el cuadro de búsqueda de paleta Hola.)

4. Busque y arrastre hello [entrenar modelo] [ train-model] toohello módulo experimentar lienzo. Conecte la salida de hello de hello [regresión lineal] [ linear-regression] toohello módulo deja la entrada del programa Hola a [entrenar modelo] [ train-model] módulo y conecte Hola entrenamiento de salida de datos (puerto de la izquierda) de hello [dividir datos] [ split] entrada derecha de módulo toohello de hello [entrenar modelo] [ train-model] módulo.

    ![Conecte Hola "Entrenar modelo" módulo tooboth Hola "Regresión lineal" y "Dividir datos de" los módulos][connect-train-model]
    <br/>
    ***Conecte Hola "Entrenar modelo" módulo tooboth Hola "Regresión lineal" y "Dividir datos de" los módulos***

5. Haga clic en hello [entrenar modelo] [ train-model] módulo, haga clic en **selector de columna de inicio** en hello **propiedades** panel y, a continuación, seleccione hello **precio** columna. Se trata de valor de Hola que nuestro modelo es toopredict continuo.

    Seleccione hello **precio** columna en el selector de columnas de hello moviendo de hello **columnas disponibles** lista toohello **columnas seleccionadas** lista.

    ![Seleccionar columna de precio de hello para el módulo de "Entrenar modelo" hello][select-price-column]
    <br/>
    ***Seleccionar columna de precio de hello para el módulo de "Entrenar modelo" hello***

6. Ejecute el experimento de Hola.

Ahora tenemos un modelo de regresión entrenado que puede ser usado tooscore nuevas automóviles toomake precio predicciones de datos.

![Después de ejecutar, experimento Hola ahora debe ser similar al siguiente][second-experiment-run]
<br/>
***Después de ejecutar, experimento Hola ahora debe ser similar al siguiente***

## <a name="step-5-predict-new-automobile-prices"></a>Paso 5: Predecir los precios de los automóviles nuevos

Ahora que nos hemos entrenar modelo de hello con 75 por ciento de los datos, podemos utilizarla tooscore Hola otros 25 por ciento de la medida de hello datos toosee nuestras funciones de modelo.

1. Busque y arrastre hello [puntuar modelo] [ score-model] toohello módulo experimentar lienzo. Conecte la salida de hello de hello [entrenar modelo] [ train-model] toohello módulo dejado el puerto de entrada de [puntuar modelo][score-model]. Conecte Hola prueba datos salida (puerto derecha) de hello [dividir datos] [ split] puerto de entrada de módulo toohello derecha [puntuar modelo][score-model].

    ![Conecte Hola "Modelo de puntuación" módulo tooboth Hola "Entrenar modelo" y "Dividir datos de" los módulos][connect-score-model]
    <br/>
    ***Conecte Hola "Modelo de puntuación" módulo tooboth Hola "Entrenar modelo" y "Dividir datos de" los módulos***

2. Ejecute el experimento de Hola y ver la salida de hello de hello [puntuar modelo] [ score-model] módulo (haga clic en el puerto de salida de hello de [puntuar modelo] [ score-model] y seleccione **Visualizar**). muestra del resultado de Hello Hola valores predichos por precio y Hola valores conocidos de datos de prueba de saludo.  

    ![Salida de hello "Modelo de puntuación" módulo][score-model-output]
    <br/>
    ***Salida de hello "Modelo de puntuación" módulo***

3. Por último, probamos calidad Hola de resultados de Hola. Seleccione y arrastre hello [evaluar modelo] [ evaluate-model] toohello módulo experimentar lienzo y conecte la salida de hello de hello [puntuar modelo] [ score-model] toohello módulo dejado de entrada de [evaluar modelo][evaluate-model].

    > [!TIP]
    > Hay dos puertos de entrada en hello [evaluar modelo] [ evaluate-model] módulo porque puede ser usado toocompare dos modelos en paralelo. Más adelante, puede agregar otro experimento de toohello de algoritmo y usar [evaluar modelo] [ evaluate-model] toosee cuál ofrece mejores resultados.

4. Ejecute el experimento de Hola.

salida de hello tooview de hello [evaluar modelo] [ evaluate-model] módulo, haga clic en el puerto de salida de hello y, a continuación, seleccione **visualizar**.

![Resultados de la evaluación de experimento Hola][evaluation-results]
<br/>
***Resultados de la evaluación de experimento Hola***

Hola siguiendo las estadísticas se muestra para nuestro modelo:

- **Desviación Media** (MAE): Hola promedio de errores absolutos (un *error* Hola diferencia entre Hola predecir el valor y el valor real de hello).
- **Raíz del Error cuadrático significa** (RMSE): raíz cuadrada de Hola de Media de Hola de errores al cuadrado de predicciones realizadas en el conjunto de datos de prueba de Hola.
- **Error absoluto relativo**: Hola promedio de errores absoluta toohello relativo absoluto de la diferencia entre los valores reales y el promedio de Hola de todos los valores reales.
- **Error cuadrático relativo**: promedio de Hola de errores al cuadrado relativo toohello cuadrado diferencia entre los valores reales de Hola y el promedio de Hola de todos los valores reales.
- **Coeficiente de determinación**: también se denomina hello **R cuadrado valor**, se trata de una métrica de estadística que indica el grado en que un modelo se adapta a los datos de Hola.

Para cada uno de los errores de hello estadísticas, menor es mejor. Un valor inferior indica que las predicciones de hello hacerlos coincidir con los valores reales de Hola. Para **coeficiente de determinación**, hello más cerca su valor es tooone (1.0), mejores predicciones de Hola Hola.

## <a name="final-experiment"></a>Experimento final

experimento final Hola debe tener un aspecto similar al siguiente:

![experimento final Hola][complete-linear-regression-experiment]
<br/>
***experimento final Hola***

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha completado el primer tutorial de aprendizaje de máquina hello y tienen su experimento configurado, puede seguir el modelo de hello tooimprove y, a continuación, implementarlo como un servicio web de predicción.

- **Recorrer en el modelo de hello tooimprove tootry** -por ejemplo, puede cambiar las características de Hola que usar en la predicción. O puede modificar las propiedades de Hola de hello [regresión lineal] [ linear-regression] algoritmo o intente un algoritmo diferente por completo. Incluso puede agregar varios equipos al mismo tiempo los algoritmos tooyour experimento de aprendizaje y comparar dos de ellos utilizando hello [evaluar modelo] [ evaluate-model] módulo.
Para obtener un ejemplo de cómo toocompare varios modelos en un experimento único, vea [comparación de regresores](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy alguna iteración del experimento, use hello **SAVE AS** situado en la parte inferior de Hola de página de Hola. Puede ver todas las iteraciones de Hola de su experimento haciendo clic en **ver el historial de ejecución** final Hola de página Hola. Para más información, consulte [Administración de iteraciones de experimentos en Azure Machine Learning Studio][runhistory].

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Implementar modelo Hola como un servicio web de predicción** : cuando esté satisfecho con el modelo, puede implementar como un toobe de servicio web utiliza los precios de automóviles toopredict mediante el uso de nuevos datos. Para más información, consulte [Implementar un servicio web Azure Machine Learning][publish].

[publish]: machine-learning-publish-a-machine-learning-web-service.md

¿Desea toolearn más? Para ver un tutorial más amplio y detallado del proceso de Hola de crear, entrenamiento, puntuación e implementar un modelo, vea [desarrollar una solución de predicción mediante aprendizaje automático de Azure][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
