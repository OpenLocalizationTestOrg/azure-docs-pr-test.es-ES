---
title: "datos de aaaAnalyze con aprendizaje automático de Azure | Documentos de Microsoft"
description: "Usar aprendizaje toobuild un modelo basado en datos almacenados en el almacén de datos de SQL Azure de aprendizaje de automático predictivo."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Análisis de datos con Aprendizaje automático de Azure
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial usa aprendizaje toobuild un modelo basado en datos almacenados en el almacén de datos de SQL Azure de aprendizaje de automático predictivo. En concreto, esto crea una campaña de marketing de Adventure Works, tienda de bicicletas de hello, predecir si un cliente es toobuy probablemente una bicicleta o no.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tutorial, necesitará:

* Una instancia de Almacenamiento de datos SQL con la base de datos de ejemplo AdventureWorksDW previamente cargada. tooprovision, vea [crear un almacén de datos de SQL] [ Create a SQL Data Warehouse] y elegir los datos de ejemplo de Hola tooload. Si ya tiene un almacenamiento de datos pero no tiene datos de ejemplo, puede [cargar manualmente los datos de ejemplo][load sample data manually].

## <a name="1-get-hello-data"></a>1. Obtener datos de Hola
datos de Hello están en la vista de dbo.vTargetMail de hello en la base de datos de hello AdventureWorksDW. tooread estos datos:

1. Inicie sesión en [Azure Machine Learning Studio][Azure Machine Learning studio] y haga clic en mis experimentos.
2. Haga clic en **+NUEVO** y seleccione **Experimento en blanco**.
3. Escriba un nombre para el experimento: Targeted Marketing.
4. Hola arrastre **lector** módulo desde el panel módulos de hello en el lienzo de Hola.
5. Especifique los detalles de hello de la base de datos de almacenamiento de datos SQL en el panel de propiedades de Hola.
6. Especifique la base de datos de hello **consulta** tooread datos de saludo de interés.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Ejecute el experimento de hello haciendo clic en **ejecutar** en el lienzo del experimento de Hola.
![Ejecute el experimento de Hola][1]

Una vez experimento Hola termina de ejecutarse correctamente, haga clic en el puerto de salida de hello en parte inferior de Hola de módulo de lector de Hola y seleccione **visualizar** toosee Hola importó los datos.
![Ver los datos importados][3]

## <a name="2-clean-hello-data"></a>2. Datos limpios Hola
datos de hello tooclean, quite algunas columnas que no son relevantes para el modelo de Hola. toodo esto:

1. Hola arrastre **proyectar columnas** módulo en el lienzo de Hola.
2. Haga clic en **selector de columna de inicio** en toospecify de panel de propiedades de hello qué columnas desea toodrop.
   ![Columnas del proyecto][4]
3. Excluya dos columnas: CustomerAlternateKey y GeographyKey.
   ![Quitar las columnas innecesariass][5]

## <a name="3-build-hello-model"></a>3. Generar modelo Hola
Dividiremos Hola datos 80: 20: 80% tootrain un modelo de aprendizaje automático y 20% tootest Hola modelo. Se hará uso de algoritmos de "Dos clases" hello para este problema de clasificación binaria.

1. Hola arrastre **división** módulo en el lienzo de Hola.
2. Escriba 0,8 de fracción de filas de hello primera salida dataset en el panel de propiedades de Hola.
   ![Dividir los datos en conjunto de entrenamiento y prueba][6]
3. Hola arrastre **árbol de decisión impulsado de dos clases** módulo en el lienzo de Hola.
4. Hola arrastre **entrenar modelo** módulo a Hola lienzo y especificar las entradas de Hola. A continuación, haga clic en **selector de columna de inicio** en el panel de propiedades de Hola.
   * Primera entrada: el algoritmo de aprendizaje automático.
   * Segunda entrada: datos tootrain Hola algoritmo.
     ![Conectar el módulo entrenar modelo de Hola][7]
5. Seleccione hello **BikeBuyer** columna Hola toopredict de columna.
   ![Seleccionar columna toopredict][8]

## <a name="4-score-hello-model"></a>4. Modelo de Hola de puntuación
Ahora, se probará cómo se comporta el modelo de hello en datos de prueba. Se comparará el algoritmo de Hola de nuestra opción con un toosee algoritmo diferente que funciona mejor.

1. Arrastre **puntuar modelo** módulo en el lienzo de Hola.
    Primera entrada: entrenar modelo segunda entrada: datos de prueba ![modelo Hola de puntuación][9]
2. Hola arrastre **máquina del punto de Bayes de dos clases** en el lienzo del experimento de Hola. Compararemos cómo realiza este algoritmo de comparación toohello árbol de decisión impulsado de dos clases.
3. Copiar y pegar Hola módulos entrenar modelo y el modelo de puntuación de hello del lienzo.
4. Hola arrastre **evaluar modelo** módulo en algoritmos de hello lienzo toocompare Hola dos.
5. **Ejecutar** Hola experimento.
   ![Ejecute el experimento de Hola][10]
6. Haga clic en el puerto de salida de hello en parte inferior de Hola de módulo de evaluar modelo hello y haga clic en visualizar.
   ![Visualizar los resultados de evaluación][11]

métricas de Hello proporcionadas son curva ROC hello, diagrama de retirada de precisión y curva de elevación. Examinar estas métricas, podemos ver ese modelo primera Hola funcionaba mejor de Hola a otra. toolook en hello qué Hola primer modelo predicha, haga clic en el puerto de salida de hello puntuar modelo y haga clic en visualizar.
![Visualizar los resultados de puntuación][12]

Verá que dos columnas más agregan conjunto de datos de prueba de tooyour.

* Probabilidades con puntuación: probabilidad de Hola que es un cliente compre una bicicleta.
* Etiquetas con puntuación: Hola clasificación realizado modelo hello: bicicleta (1) o no (0). Este umbral de probabilidad para etiquetar se establece too50% y se puede ajustar.

Comparando Hola columna BikeBuyer (real) con las etiquetas con puntuación de hello (predicción), puede ver la medida ha realizado el modelo de Hola. Como los pasos siguientes, puede usar este predicciones de toomake de modelo para los nuevos clientes y publicar este modelo como un servicio web o escribir resultados atrás tooSQL almacenamiento de datos.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de crear modelos de aprendizaje de automático predictivo consulte demasiado[tooMachine de introducción de aprendizaje en Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
