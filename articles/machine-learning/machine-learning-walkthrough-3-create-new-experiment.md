---
title: "Paso 3: Creación de un nuevo experimento de Machine Learning | Microsoft Docs"
description: "Paso 3 del programa Hola a desarrollar un solución de predicción Tutorial: crear un nuevo experimento de entrenamiento en estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Paso 3 del tutorial: Creación de un nuevo experimento de Aprendizaje automático de Azure
Esto es Hola tercer paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carga de los datos existentes](machine-learning-walkthrough-2-upload-data.md)
3. **Crear un experimento nuevo**
4. [Entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implementar el servicio Web de Hola](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acceder al servicio Web Hola](machine-learning-walkthrough-6-access-web-service.md)

- - -
Hola siguiente paso en este tutorial es toocreate un experimento en estudio de aprendizaje automático que utiliza el conjunto de datos de Hola que se cargan.  

1. En Studio, haga clic en **+ nuevo** final Hola de ventana hello.
2. Seleccione **EXPERIMENTO**y luego "Experimento en blanco". 

    ![Creación de un nuevo experimento][0]

2. Predeterminado de hello seleccione experimentar nombre en parte superior de hello del lienzo de Hola y cambie su nombre toosomething significativo.

    ![Renombrar el experimento][5]
   
   > [!TIP]
   > Es una buena práctica toofill **resumen** y **descripción** para experimento Hola Hola **propiedades** panel. Estos proporcionan propiedades Hola experimento de hello toodocument oportunidad para que cualquier persona que examina más adelante puedan comprender los objetivos y la metodología.
   > 
   > ![Propiedades del experimento][6]
   > 
3. En hello módulo paleta toohello izquierda del lienzo del experimento de hello expanda **conjuntos de datos guardados**.
4. Conjunto de datos de Hola de búsqueda que ha creado en **Mis conjuntos de datos** y lo arrastra al lienzo de Hola. También puede encontrar el conjunto de datos de hello escribiendo el nombre de Hola Hola **búsqueda** cuadro situado encima de la paleta de Hola.  

    ![Agregar toohello experimento de hello conjunto de datos][7]

## <a name="prepare-hello-data"></a>Preparar los datos de Hola
Puede ver hello las 100 primeras filas de datos de Hola y determinados datos estadísticos para hello todo el conjunto de datos: haga clic en el puerto de salida de hello del conjunto de datos de hello (Hola pequeño círculo final Hola) y seleccione **visualizar**.  

Porque el archivo de datos de hello no incluye encabezados de columna, Studio ha proporcionado encabezados genéricos (Col1, Col2, *etc.*). Encabezados de buena no son esencial toocreating un modelo, pero hacen que sea más fácil toowork con datos de hello en el experimento de Hola. Además, cuando finalmente se publica este modelo en un servicio web, encabezados de hello ayudar a identificar Hola columnas toohello usuario del servicio de Hola.  

Podemos agregar encabezados de columna con hello [editar metadatos] [ edit-metadata] módulo.
Usar hello [editar metadatos] [ edit-metadata] módulo toochange metadatos asociados a un conjunto de datos. En este caso, usamos lo tooprovide nombres más descriptivos para los encabezados de columna. 

toouse [editar metadatos][edit-metadata], especifique primero qué toomodify columnas (en este caso, todas ellas.) A continuación, especificar Hola acción toobe realizada en esas columnas (en este caso, cambiar los encabezados de columna.)

1. En la paleta de módulo de hello, escriba "metadatos" Hola **búsqueda** cuadro. Hola [editar metadatos] [ edit-metadata] aparece en la lista de módulos de Hola.

2. Haga clic y arrastre hello [editar metadatos] [ edit-metadata] módulo en hello lienzo y colóquela debajo de conjunto de datos de Hola se agregó anteriormente.

3. Conectar Hola dataset toohello [editar metadatos][edit-metadata]: haga clic en el puerto de salida de hello del conjunto de datos de hello (Hola pequeño círculo final Hola del conjunto de datos de hello), arrastre toohello el puerto de entrada de [editar metadatos ] [ edit-metadata] (Hola pequeño círculo en parte superior de hello del módulo de hello), a continuación, suelte el botón del mouse de Hola. módulo y un conjunto de hello permanecen conectadas aun cuando que se recorre ya sea en el lienzo de Hola.
   
   el experimento de Hello ahora debería ser similar al siguiente:  
   
   ![Agregar metadatos de edición][1]
   
   marca de exclamación Hola rojo indica que no hemos configurado aún las propiedades de Hola para este módulo. Lo haremos a continuación.
   
   > [!TIP]
   > Puede agregar un módulo tooa comentario haciendo doble clic en módulo de Hola y de escritura de texto. Esto puede ayudarle a ver de un vistazo qué módulo Hola está haciendo en el experimento. En este caso, haga doble clic en hello [editar metadatos] [ edit-metadata] módulo y tipo hello comentario "Agregar encabezados de columna". Haga clic en ningún otro lugar en cuadro de texto de hello lienzo tooclose Hola. toodisplay Hola comentario, haga clic en la flecha abajo de hello en el módulo de Hola.
   > 
   > ![Modificación del módulo de metadatos con el comentario agregado][8]
   > 
4. Seleccione [editar metadatos][edit-metadata]y en hello **propiedades** toohello del panel derecho del lienzo de hello, haga clic en **selector de columna de inicio**.

5. Hola **seleccionar columnas** cuadro de diálogo, seleccione todas las filas de Hola **columnas disponibles** y haga clic en > toomove ellos demasiado**columnas seleccionadas**.
   cuadro de diálogo de Hello debería tener este aspecto:

   ![Selector de columnas con todas las columnas seleccionadas][2]

6. Haga clic en hello **Aceptar** marca de verificación.

7. Nuevo en hello **propiedades** panel, busque hello **nuevos nombres de columna** parámetro. En este campo, escriba una lista de nombres para hello 21 columnas de conjunto de datos de hello, separados por comas y en orden de las columnas. Puede obtener los nombres de las columnas de Hola de documentación de conjunto de datos de hello en el sitio Web UCI hello, o para su comodidad puede copiar y pegar Hola lista siguiente:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   panel de propiedades de Hello tiene el siguiente aspecto:
   
   ![Propiedades de los metadatos de edición][3]

> [!TIP]
> Si desea que los encabezados de columna de hello tooverify, ejecute el experimento de hello (haga clic en **ejecutar** por debajo del lienzo del experimento de hello). Cuando finaliza la ejecución (aparece una marca de verificación verde en [editar metadatos][edit-metadata]), haga clic en el puerto de salida de hello de hello [editar metadatos] [ edit-metadata] módulo y seleccione **visualizar**. Puede ver la salida de hello de cualquier módulo Hola mismo progreso de hello tooview de forma de datos de Hola a través de experimento Hola.
> 
> 

## <a name="create-training-and-test-datasets"></a>Creación de conjuntos de datos de entrenamiento y prueba
Necesitamos algunos modelos de datos tootrain hello y algunos tootest se.
Por lo que en el paso siguiente de hello del experimento de hello, dividiremos Hola conjunto de datos en dos conjuntos de datos independientes: uno para el entrenamiento de nuestro modelo y otro para probarlo.

toodo, usamos hello [dividir datos] [ split] módulo.  

1. Buscar hello [dividir datos] [ split] módulo, arrástrelo al lienzo de Hola y conéctela toohello [editar metadatos] [ edit-metadata] módulo.

2. De forma predeterminada, relación de división de hello es 0,5 y hello **división aleatorio** parámetro está establecido. Esto significa que una mitad aleatoria de datos de hello es la salida a través de un puerto de hello [dividir datos] [ split] mitad hello a otro y módulo. Puede ajustar estos parámetros, así como Hola **valor de inicialización aleatorio** parámetro, hello toochange dividido entre los datos de pruebas y entrenamiento. En este ejemplo, se deja tal cual.
   
   > [!TIP]
   > Hola propiedad **fracción de filas de hello en primer lugar de conjunto de datos de salida** determina la cantidad de datos de hello salida a través de hello es *izquierdo* puerto de salida. Por ejemplo, si establece too0.7 de proporción de hello, salida a través de hello dejado de puerto y 30% a través del puerto derecha hello es 70% de los datos de Hola.  
   > 
   > 

3. Haga doble clic en hello [dividir datos] [ split] módulo y escriba el comentario de hello, "datos de entrenamiento y prueba división 50%". 

Podemos usar salidas Hola de hello [dividir datos] [ split] módulo sin embargo nos gusta, pero vamos a seleccionar toouse Hola izquierdo se muestran como datos de entrenamiento y Hola directamente los datos como pruebas de salida.  

Como se mencionó en hello [paso anterior](machine-learning-walkthrough-2-upload-data.md), costo de Hola de clasifique mal un riesgo de crédito alta como baja es cinco veces mayor que el costo de Hola de clasifique mal un riesgo de crédito baja como high. tooaccount para esto, se genera un nuevo conjunto de datos que refleja esta función de costo. Hola nuevo conjunto de datos, cada ejemplo de alto riesgo se replica cinco veces, mientras no se replica en cada ejemplo de bajo riesgo.   

Podemos conseguir esta replicación mediante el código R:  

1. Busque y arrastre hello [ejecutar Script de R] [ execute-r-script] módulo al lienzo del experimento de Hola. 

2. Conectar Hola dejado el puerto de salida de hello [dividir datos] [ split] toohello módulo primera entrada de puerto ("Dataset1") del programa Hola a [ejecutar Script de R] [ execute-r-script] módulo.

3. Haga doble clic en hello [ejecutar Script de R] [ execute-r-script] módulo y escriba el comentario de hello, "Ajuste del coste de conjunto".

4. Hola **propiedades** panel, el texto de eliminación Hola predeterminado en hello **Script de R** parámetro y escriba esta secuencia de comandos:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script de R en el módulo ejecutar Script de R de Hola][9]

Necesitamos toodo esta misma operación de replicación para cada salida de hello [dividir datos] [ split] ajuste del módulo para ese Hola de entrenamiento y de datos de prueba ha Hola mismo costo. Hola toodo de manera más sencilla es duplicando hello [ejecutar Script de R] [ execute-r-script] módulo se acaba de crear y conectar toohello salida otro puerto de hello [dividir datos de] [ split] módulo.

1. Menú contextual hello [ejecutar Script de R] [ execute-r-script] módulo y seleccione **copia**.

2. Haga clic en el lienzo del experimento de Hola y seleccione **pegar**.

3. Arrastre el nuevo módulo de hello en su posición y, a continuación, conecte el puerto de salida derecho de Hola de hello [dividir datos] [ split] toohello módulo primera entrada de puerto de este nuevo [ejecutar Script de R] [ execute-r-script] módulo. 

4. En la parte inferior de hello del lienzo de hello, haga clic en **ejecutar**. 

> [!TIP]
> copia de Hola de módulo ejecutar Script de R de hello contiene Hola mismo script como módulo original de Hola. Al copiar y pegar un módulo en el lienzo de hello, copia de hello conserva todas las propiedades de Hola de hello original.  
> 
> 

Nuestro experimento tiene ahora un aspecto similar al siguiente:

![Adding Split module and R scripts][4]

Para obtener más información sobre cómo usar los scripts de R en sus experimentos, consulte [Extender el experimento con R](machine-learning-extend-your-experiment-with-r.md).

**Siguiente: [entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
