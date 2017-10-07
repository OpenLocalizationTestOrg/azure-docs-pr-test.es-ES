---
title: aaaCreate varios modelos de un experimento | Documentos de Microsoft
description: "Usar PowerShell toocreate varios modelos de aprendizaje automático y extremos de servicio con hello web mismo algoritmo, pero los conjuntos de datos de entrenamiento diferentes."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Creación de varios modelos de aprendizaje automático y puntos de conexión de servicio web a partir de un experimento mediante PowerShell
Este es un problema común de aprendizaje de máquina: desea toocreate muchos modelos que tienen Hola mismo flujo de trabajo de aprendizaje y uso Hola mismo algoritmo, pero tienen conjuntos de datos de entrenamiento diferente como entrada. Este artículo muestra cómo toodo esto a escala en estudio de aprendizaje automático de Azure con un experimento de único.

Por ejemplo, digamos que posee una empresa de franquicias de alquiler de bicicletas global. Desea toobuild una petición de alquiler de regresión modelo toopredict Hola basada en datos históricos. Dispone de 1.000 ubicaciones de alquiler a través de Hola a todos y que ha recopilado un conjunto de datos para cada ubicación que incluye características importantes como fecha, hora, el tiempo y el tráfico que son específicos tooeach ubicación.

Podría entrenar el modelo una vez usando una versión combinada de todos los conjuntos de datos de hello en todas las ubicaciones. Pero dado que cada una de las ubicaciones tiene un entorno único, un mejor enfoque podría ser tootrain el modelo de regresión por separado con el conjunto de datos de Hola para cada ubicación. De este modo, cada modelo entrenado puede tardar en tamaños de almacén diferente de cuenta hello, volumen, geography, rellenado, entorno de tráfico de bicicleta sencillo, *etc.*.

Que puede ser recomendable hello, pero no desea toocreate 1.000 experimentos de aprendizaje en aprendizaje automático de Azure con cada uno de ellos que representa una ubicación única. Además de ser una tarea abrumadora, también es parece bastante ineficaz, ya que cada experimento todos deberá Hola los mismos componentes excepto para el conjunto de datos de entrenamiento de Hola.

Afortunadamente, podemos realizar mediante el uso de hello [aprendizaje automático de Azure reciclaje API](machine-learning-retrain-models-programmatically.md) y automatizar tareas de hello con [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake nuestro ejemplo ejecutarse con mayor rapidez, se reducirá el número de Hola de ubicaciones de 1.000 too10. Pero hello mismos principios y procedimientos se aplican too1, 000 ubicaciones. Hola única diferencia es que si desea tootrain de conjuntos de datos de 1.000, seguramente quieras toothink de hello siguientes secuencias de comandos de PowerShell en paralelo en ejecución. ¿Cómo toodo que está más allá del ámbito de Hola de este artículo, pero puede encontrar ejemplos de PowerShell multithreading en hello Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Configurar el experimento de entrenamiento de Hola
Vamos a toouse un ejemplo [experimento de entrenamiento](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que ya hemos creado en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Abra este experimento en su área de trabajo [Estudio de aprendizaje automático de Azure](https://studio.azureml.net) .

> [!NOTE]
> En orden toofollow junto con este ejemplo, puede que desee toouse un área de trabajo estándar en lugar de un área de trabajo disponible. Se creará un punto de conexión para cada cliente - para un total de 10 puntos de conexión - y que requieren un área de trabajo estándar, puesto que un área de trabajo libre es limitado too3 extremos. Si solo tiene un área de trabajo gratuita, simplemente modifique los scripts de hello debajo tooallow para solo 3 ubicaciones.
> 
> 

experimento Hello usa un **importar datos** conjunto de datos de entrenamiento de módulo tooimport hello *customer001.csv* desde una cuenta de almacenamiento de Azure. Supongamos que hemos recopilado los conjuntos de datos de entrenamiento de todas las ubicaciones de alquiler de bicicletas y almacenado en hello misma ubicación de almacenamiento de blobs con nombres de archivo que van desde *rentalloc001.csv* demasiado*rentalloc10.csv* .

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Tenga en cuenta que un **resultado del servicio Web** módulo se ha agregado toohello **entrenar modelo** módulo.
Cuando este experimento se implementa como un servicio web, extremo de hello asociado a esa salida devolverá entrenado hello en formato de Hola de un archivo .ilearner.

Tenga en cuenta también que configuramos un parámetro del servicio web para la dirección URL de Hola que hello **importar datos** utiliza el módulo. Esto nos permite toouse Hola parámetro toospecify individuales conjuntos de datos tootrain Hola modelo de entrenamiento para cada ubicación.
Hay otras maneras podríamos haber hecho esto, por ejemplo, mediante una consulta SQL con una web servicio parámetro tooget los datos de una base de datos de SQL Azure, o simplemente con una **proporcionados por el servicio Web** toopass de módulo en un conjunto de datos toohello de servicio web.

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Ahora, vamos a ejecutar este experimento de entrenamiento con el valor predeterminado de hello *rental001.csv* como Hola conjunto de datos de entrenamiento. Si ve la salida de hello de hello **Evaluate** módulo (haga clic en salida de hello y seleccione **visualizar**), puede ver que obtenemos un rendimiento aceptable de *AUC* = 0.91. En este momento, estamos listo toodeploy un servicio web fuera de este experimento de entrenamiento.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Implementar el entrenamiento de Hola y de puntuación de servicios web
Hola toodeploy entrenamiento servicio web, haga clic en hello **configurar el servicio de Web** situado por debajo del lienzo del experimento de Hola y seleccione **implementar servicio Web**. Llame a este servicio web "Bike Rental Training" (Entrenamiento para alquiler de bicicletas).

Ahora necesitamos servicio toodeploy Hola de puntuación web.
toodo, podemos hacer clic en **configurar el servicio de Web** por debajo de hello lienzo y seleccione **predictivo servicio Web**. Esto crear un experimento de puntuación.
Necesitaremos toomake unos toomake ajustes menores funciona como un servicio web, como datos de entrada de quitar la columna de etiqueta de Hola "cnt" de Hola y limitar el Id. de instancia de hello salida tooonly Hola y Hola correspondiente predice el valor.

toosave usted mismo que el trabajo, podrá abrirlo hello [experimento predictivo](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) Hola galería que ya se ha preparado.

servicio web de toodeploy hello, ejecute hello experimento predictivo, a continuación, haga clic en hello **implementar el servicio de Web** botón a continuación lienzo Hola. Hola de nombre la puntuación del servicio web "Puntuación de alquiler de bicicletas" ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Creación de 10 puntos de conexión de servicio web idénticos con PowerShell
Este servicio web incluye un punto de conexión predeterminado. Pero nos no interesa como punto de conexión de hello predeterminado porque no se puede actualizar. Lo que necesitamos toodo es toocreate 10 extremos adicionales, uno para cada ubicación. Haremos esto con PowerShell.

En primer lugar, configure nuestro entorno de PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

A continuación, ejecute el siguiente comando de PowerShell de hello:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Ahora que hemos creado 10 puntos de conexión y contienen Hola mismo modelo entrenado se entrenó en *customer001.csv*. Puede verlos en hello Portal de administración de Azure.

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Actualizar Hola extremos toouse entrenamiento independiente conjuntos de datos mediante PowerShell
Hola siguiente paso es extremos de hello tooupdate con modelos de que forma única se entrenó en datos individuales de cada cliente. Pero primero necesitamos tooproduce estos modelos de hello **entrenamiento de alquiler de bicicletas** servicio web. Volvamos atrás toohello **entrenamiento de alquiler de bicicletas** servicio web. Necesitamos toocall su extremo BES 10 veces con 10 conjuntos de datos de entrenamiento diferentes en modelos diferentes de orden tooproduce 10. Vamos a usar hello **InovkeAmlWebServiceBESEndpoint** toodo de cmdlet de PowerShell esto.

También necesitará tooprovide credenciales para la cuenta de almacenamiento de blobs en `$configContent`, es decir, en los campos de hello `AccountName`, `AccountKey` y `RelativeLocation`. Hola `AccountName` puede ser uno de los nombres de cuenta, como se muestra en hello **Portal de administración de Azure clásico** (*almacenamiento* ficha). Cuando hace clic en una cuenta de almacenamiento, su `AccountKey` encontrará presionando hello **administrar claves de acceso** situado en la parte inferior de Hola y copiar hello *clave de acceso principal*. Hola `RelativeLocation` es el almacenamiento de información de hello ruta de acceso relativa tooyour donde se almacenará un nuevo modelo. Por ejemplo, ruta de acceso de hello `hai/retrain/bike_rental/` en script de Hola puntos tooa contenedor denominado `hai`, y `/retrain/bike_rental/` son subcarpetas. Actualmente, no se puede crear subcarpetas a través de la interfaz de usuario del portal de hello, pero hay [varios exploradores de almacenamiento de Azure](../storage/common/storage-explorers.md) que le permiten toodo así. Se recomienda crear un nuevo contenedor en el saludo de toostore de almacenamiento nuevos modelos entrenados (archivos .ilearner) como sigue: desde la página de almacenamiento, haga clic en hello **agregar** situado en la parte inferior de Hola y asígnele el nombre `retrain`. En resumen, Hola cambios necesarios toohello siguiente secuencia de comandos pertenecen demasiado`AccountName`, `AccountKey` y `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> Hola extremo BES es Hola solo admite el modo para esta operación. RRS no se puede usar para generar modelos entrenados.
> 
> 

Como puede ver más arriba, en lugar de construir 10 diferentes BES trabajo json archivos de configuración, creamos dinámicamente cadena_configuración hello en su lugar y fuente toohello *jobConfigString* parámetro de hello  **InvokeAmlWebServceBESEndpoint** cmdlet, puesto que no hay realmente ningún tookeep necesidad de una copia en el disco.

Si todo va bien, después de un tiempo, debe ver 10 archivos .ilearner, de *model001.ilearner* demasiado*model010.ilearner*, en su cuenta de almacenamiento de Azure. Ahora estamos listo tooupdate nuestro 10 puntuación web los extremos del servicio con estos modelos mediante hello **AmlWebServiceEndpoint revisión** cmdlet de PowerShell. Nuevo, recuerde que sólo le podemos patch puntos de conexión de hello no predeterminada que se crea mediante programación anteriormente.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

Esto se debe ejecutar bastante rápido. Cuando concluya la ejecución de hello, se habrá creado correctamente 10 puntos de conexión de servicio de web de predicción, cada uno con un modelo entrenado entrenado forma única en la ubicación de alquiler de tooa específico de hello conjunto de datos, todo ello desde un experimento de entrenamiento único. tooverify esto, puede intentar llamar a estos extremos con hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, enviarles con hello los mismos datos de entrada, y debe esperar resultados de predicción diferentes toosee puesto que son modelos de Hola entrenado con conjuntos de entrenamiento diferentes.

## <a name="full-powershell-script"></a>Script de PowerShell completo
Este es el anuncio de Hola de código fuente completo de Hola:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
