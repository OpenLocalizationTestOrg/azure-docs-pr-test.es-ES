---
title: "aaaUsing datos de importación y exportación en los servicios web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola toosend de módulos de importación de datos y exportar datos y recibir datos de un servicio web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Implementación de servicios web del aprendizaje automático de Azure que usan módulos de importación y exportación de datos

Cuando se crea un experimento predictivo, normalmente se agregan una entrada y una salida de servicio web. Cuando se implementa el experimento de hello, los consumidores pueden enviar y recibir datos del servicio web de Hola a través de hello entradas y salidas. En algunas aplicaciones, los datos del consumidor pueden estar disponibles desde una fuente de datos o ya residir en un origen de datos externo, como el Almacenamiento de blobs de Azure. En estos casos, no se requiere que lean y escriban datos mediante entradas y salidas del servicio web. En su lugar, puede usar datos de tooread de servicio de ejecución de lotes (BES) de Hola Hola origen de datos mediante un módulo de importación de datos y escribir hello tooa ubicación de datos diferente mediante un módulo de exportar datos de resultados de puntuación.

Hello importar datos y módulos de exportación de datos, puede leer y escribir datos toovarious proporcionan ubicaciones como una dirección URL Web a través de HTTP, una consulta de Hive, una base de datos SQL de Azure, almacenamiento de tabla de Azure, almacenamiento de blobs de Azure, una fuente de datos o una base de datos SQL local.

En este tema usa Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" de ejemplo y se da por supuesto Hola conjunto de datos ya se han cargado en una tabla de SQL Azure denominada censusdata.

## <a name="create-hello-training-experiment"></a>Crear experimento de entrenamiento de Hola
Cuando abre Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" ejemplo de conjunto de datos utiliza Hola ejemplo clasificación binaria de ingresos del censo para adultos. Y experimento hello en el lienzo de hello tendrá un aspecto similar toohello después de imagen:

![Configuración inicial del experimento de Hola.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

datos de hello tooread de tabla de SQL Azure hello:

1. Eliminar el módulo de conjunto de datos de Hola.
2. En el cuadro de búsqueda de componentes de hello, tipo de importación.
3. Desde la lista de resultados de hello, agregar un *importar datos* toohello módulo experimentar lienzo.
4. Conecte la salida de hello *importar datos* entrada de módulo Hola de hello *limpiar datos que faltan* módulo.
5. En el panel Propiedades, seleccione **base de datos de SQL Azure** en hello **origen de datos** lista desplegable.
6. Hola **el nombre del servidor de base de datos**, **nombre de base de datos**, **nombre de usuario**, y **contraseña** campos, especifique la información adecuada de Hola para la base de datos.
7. En el campo de consulta de base de datos de hello, escriba Hola después de consulta.
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.

## <a name="create-hello-predictive-experiment"></a>Crear experimento predictivo Hola
Después de que configurar experimento predictivo Hola desde el que implementa el servicio web.

1. En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **predictivo Web Service [recomendado]**.
2. Quitar hello *proporcionados por el servicio Web* y *módulos de salida del servicio Web* de experimento predictivo Hola. 
3. En el cuadro de búsqueda de componentes de hello, tipo de exportación.
4. Desde la lista de resultados de hello, agregar un *exportar datos* toohello módulo experimentar lienzo.
5. Conecte la salida de hello *puntuar modelo* entrada de módulo Hola de hello *exportar datos* módulo. 
6. En el panel Propiedades, seleccione **base de datos de SQL Azure** en la lista desplegable destino de datos de Hola.
7. Hola **el nombre del servidor de base de datos**, **nombre de base de datos**, **nombre de cuenta de usuario de servidor**, y **contraseña de cuenta de usuario de servidor** campos, escriba información adecuada de Hello para la base de datos.
8. Hola **lista de toobe columnas guarda separada por comas** , escriba la puntuación de etiquetas.
9. Hola **campo de nombre de tabla de datos**, escriba dbo. ScoredLabels. Si la tabla hello no existe, se crea cuando se ejecuta el experimento de Hola o se llama servicio de web de Hola.
10. Hola **lista de columnas de tabla de datos separada por comas** campo, escriba ScoredLabels.

Cuando se escribe una aplicación que llama Hola servicio web final, puede que desee toospecify una tabla de consulta o el destino entrada diferente en tiempo de ejecución. tooconfigure estas entradas y salidas, utilice Hola Hola de tooset de característica de parámetros de servicio Web *importar datos* módulo *origen de datos* hello y propiedad *exportar datos* modo propiedad de destino de datos.  Para obtener más información sobre los parámetros del servicio Web, vea hello [entrada de parámetros de servicio Web de aprendizaje automático de Azure](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) en hello Intelligence Cortana y el Blog de aprendizaje automático.

tooconfigure Hola parámetros de servicio Web de consulta de importación de Hola y tabla de destino de hello:

1. En panel de propiedades de Hola de hello *importar datos* módulo, haga clic en el icono de hello en hello parte superior derecha de hello **consulta de base de datos** campo y seleccione **establecer como parámetro del servicio web**.
2. En panel de propiedades de Hola de hello *exportar datos* módulo, haga clic en el icono de hello en hello parte superior derecha de hello **nombre de la tabla de datos** campo y seleccione **establecer como parámetro del servicio web**.
3. En parte inferior de Hola de hello *exportar datos* panel de propiedades de módulo, en hello **parámetros de servicio Web** sección, haga clic en la consulta de base de datos y cambie su consulta.
4. Haga clic en **Nombre de la tabla de datos** y cambie el nombre por **Table**.

Cuando haya terminado, su experimento debería ser similar toohello después de imagen:

![Aspecto final del experimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

Ahora puede implementar Hola experimento como un servicio web.

## <a name="deploy-hello-web-service"></a>Implementar el servicio web de Hola
Puede implementar tooeither un servicio web clásico o nuevo.

### <a name="deploy-a-classic-web-service"></a>Implementación de un servicio web clásico
toodeploy como un servicio Web clásico y crear una aplicación tooconsume:

1. En parte inferior de hello del lienzo del experimento de hello, haga clic en ejecutar.
2. Cuando haya finalizado Hola ejecutar, haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]**.
3. En el panel de servicio web de hello, busque la clave de API. Copie y guarde toouse más tarde.
4. Hola **punto de conexión predeterminado** de tabla, haga clic en hello **ejecución por lotes** Hola de vínculo tooopen página de Ayuda de API.
5. Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.
6. En la página de Ayuda de la API de hello, encontrar Hola **código de ejemplo** sección final Hola de página Hola.
7. Copie y pegue Hola código de ejemplo de C# en el archivo Program.cs y quitar el almacenamiento de blobs de toohello de todas las referencias.
8. Actualizar el valor de Hola de hello *apiKey* variable con clave Hola API que guardó anteriormente.
9. Busque Hola declaración y actualización Hola valores de solicitud de parámetros de servicio Web que se pasan toohello *importar datos* y *exportar datos* módulos. En este caso, utilice la consulta original de hello, pero define un nuevo nombre de tabla.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Ejecute la aplicación hello. 

En la realización de hello ejecutar, se agrega una nueva tabla toohello base de datos que contiene los resultados de puntuación de Hola.

### <a name="deploy-a-new-web-service"></a>Implementación de servicios web nuevos

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy como un nuevo servicio Web y crear una aplicación tooconsume:

1. En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.
2. Cuando haya finalizado Hola ejecutar, haga clic en **implementar el servicio de Web** y seleccione **implementar [New] servicio Web**.
3. En página de experimento implementar hello, escriba un nombre para el servicio web y seleccione un plan de precios y, a continuación, haga clic en **implementar**.
4. En hello **inicio rápido** página, haga clic en **usar**.
5. Hola **código de ejemplo** sección, haga clic en **por lotes**.
6. Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.
7. Copie y pegue el código de ejemplo de Hola C# en el archivo Program.cs.
8. Actualizar el valor de Hola de hello *apiKey* variable con hello **Primary Key** ubicado en hello **información básica de consumo** sección.
9. Busque hello *scoreRequest* declaración y actualizar valores de hello de parámetros de servicio Web que se pasan toohello *importar datos* y *exportar datos* módulos. En este caso, utilice la consulta original de hello, pero define un nuevo nombre de tabla.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Ejecute la aplicación hello. 

