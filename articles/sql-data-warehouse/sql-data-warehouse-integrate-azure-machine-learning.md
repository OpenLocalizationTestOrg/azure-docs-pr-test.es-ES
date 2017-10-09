---
title: "Aprendizaje automático de Azure con el almacenamiento de datos de SQL aaaUse | Documentos de Microsoft"
description: "Tutorial para usar Aprendizaje automático de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Uso de Aprendizaje automático de Azure con Almacenamiento de datos SQL
Aprendizaje automático de Azure es un servicio de análisis predictivos completamente administrado que puede usar modelos de predicción toocreate con sus datos en el almacén de datos de SQL y, a continuación, publicar como servicios web listos para su consumo. Puede aprender aspectos básicos de Hola de análisis predictivo y aprendizaje automático leyendo [tooMachine de introducción de aprendizaje en Azure][Introduction tooMachine Learning on Azure].  Puede obtener información sobre cómo entrenar toocreate, puntuarlos y probar un modelo de aprendizaje automático con hello [crear experimento tutorial][Create experiment tutorial].

En este artículo, aprenderá cómo hello toodo sigue utilizando hello [estudio de aprendizaje automático de Azure][Azure Machine Learning Studio]:

* Leer datos de la base de datos toocreate, entrenar y puntuar un modelo de predicción
* Escribir la base de datos de tooyour de datos

## <a name="read-data-from-sql-data-warehouse"></a>Lectura de datos desde Almacenamiento de datos SQL
Se debe leer datos de la tabla Product en la base de datos de hello AdventureWorksDW.

### <a name="step-1"></a>Paso 1
Inicie un experimento de nuevo haciendo clic en + nuevo final Hola de hello ventana de estudio de aprendizaje automático, seleccione EXPERIMENTO y, a continuación, seleccione experimentar en blanco. Predeterminado de hello seleccione experimentar nombre en parte superior de hello del lienzo de Hola y cambie su nombre toosomething significativo, por ejemplo, predicción de precio de bicicleta.

### <a name="step-2"></a>Paso 2
Busque el módulo de lector de hello en la paleta de Hola de conjuntos de datos y los módulos de izquierda Hola del lienzo del experimento de Hola. Arrastre el lienzo del experimento de hello módulo toohello.
![][drag_reader]

### <a name="step-3"></a>Paso 3
Seleccionar módulo de lector de Hola y rellenar el panel de propiedades de Hola.

1. Seleccione la base de datos de SQL Azure como Hola origen de datos.
2. Nombre del servidor de base de datos: nombre del servidor de tipo hello. Puede usar hello [portal de Azure] [ Azure portal] toofind esto.

![][server_name]

1. Nombre de base de datos: nombre de una base de datos que acaba de especificar el servidor de Hola Hola de tipo.
2. Nombre de cuenta de usuario de servidor: escriba el nombre de usuario de Hola de una cuenta que tenga permisos de acceso de la base de datos de Hola.
3. Contraseña de cuenta de usuario de servidor: proporcionar contraseña Hola Hola cuenta de usuario especificada.
4. Aceptar cualquier certificado de servidor: Utilice esta opción (menos segura) si desea tooskip revisar certificado de sitio de hello antes de leer los datos.
5. Consulta de base de datos: escriba una instrucción SQL que describe datos de Hola que desee tooread. En este caso, se debe leer datos de tabla Product mediante Hola después de consulta.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Paso 4
1. Ejecute el experimento de hello haciendo clic en ejecutar en el lienzo del experimento de Hola.
2. Cuando finaliza el experimento de hello, módulo de lector de hello tendrá un tooindicate de marca de verificación verde que se ha completado correctamente. Tenga en cuenta también Hola ha terminado de estado de ejecución en la esquina superior derecha de Hola.

![][run]

1. toosee Hola datos importados, haga clic en el puerto de salida de hello en parte inferior de hello del conjunto de datos de automóviles de Hola y seleccione visualizar.

## <a name="create-train-and-score-a-model"></a>Creación, entrenamiento y puntuación de un modelo
Ahora puede utilizar este conjunto de datos para:

* Crear un modelo: procesar datos y definir características
* Entrenar el modelo de hello: elegir y aplicar un algoritmo de aprendizaje
* Puntuación y prueba Hola modelo: predecir nuevo precio de bicicleta

![][model]

más información acerca de cómo toocreate, entrenar, puntuarlos y probar un Hola de uso del modelo de aprendizaje automático de toolearn [crear experimento tutorial][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Escribir datos tooAzure almacenamiento de datos SQL
Tabla de tooProductPriceForecast de conjunto de resultados de Hola se escribirán en la base de datos de hello AdventureWorksDW.

### <a name="step-1"></a>Paso 1
Busque el módulo de escritor de hello en la paleta de Hola de conjuntos de datos y los módulos izquierda Hola del lienzo del experimento de Hola. Arrastre el lienzo del experimento de hello módulo toohello.

![][drag_writer]

### <a name="step-2"></a>Paso 2
Seleccionar módulo de escritor de Hola y rellenar el panel de propiedades de Hola.

1. Seleccionar base de datos de SQL Azure como Hola destino de datos.
2. Nombre del servidor de base de datos: nombre del servidor de tipo hello. Puede usar hello [portal de Azure] [ Azure portal] toofind esto.
3. Nombre de base de datos: nombre de una base de datos que acaba de especificar el servidor de Hola Hola de tipo.
4. Nombre de cuenta de usuario de servidor: escriba el nombre de usuario de Hola de una cuenta que tenga permisos de escritura para la base de datos de Hola.
5. Contraseña de cuenta de usuario de servidor: proporcionar contraseña Hola Hola cuenta de usuario especificada.
6. Aceptar cualquier certificado de servidor (no seguro): seleccione esta opción si no desea certificado de hello tooview.
7. Lista separada por comas de toobe columnas guardado: proporcione una lista de columnas de conjunto de datos o el resultado de hello que desea toooutput.
8. Nombre de la tabla de datos: especifique Hola nombre de tabla de datos de Hola.
9. Lista separada por comas de las columnas de la datatable: especificar toouse de nombres de columna de hello en nueva tabla de Hola. Hello nombres de columna pueden ser diferentes de Hola que en el conjunto de datos de origen de hello, pero debe incluir Hola el mismo número de columnas aquí que se define para la tabla de salida de hello.
10. Número de filas escritas por cada operación de SQL Azure: puede configurar Hola número de filas que se escriben tooa base de datos SQL en una sola operación.

![][writer_properties]

### <a name="step-3"></a>Paso 3
1. Ejecute el experimento de hello haciendo clic en ejecutar en el lienzo del experimento de Hola.
2. Cuando finaliza el experimento de hello, todos los módulos tendrá un tooindicate de marca de verificación verde que completó correctamente.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
