---
title: "aaaRetrain aprendizaje automático se modela mediante programación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically volver a entrenar un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Volver a entrenar modelos de aprendizaje automático mediante programación
En este tutorial, aprenderá cómo tooprogrammatically volver a entrenar a un servicio de Web de aprendizaje de máquina de Azure con C# y Hola servicio de ejecución de lotes de aprendizaje de máquina.

Una vez que se vuelven a entrenar el modelo de hello, Hola siguientes tutoriales muestra cómo tooupdate Hola modelo en el servicio web de predicción:

* Si implementa un servicio web de clásico en el portal de servicios Web de aprendizaje de máquina de hello, consulte [entrenar el modelo de servicio web clásico](machine-learning-retrain-a-classic-web-service.md). 
* Si ha implementado un nuevo servicio web, consulte [volver a entrenar un nuevo servicio web mediante los cmdlets de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).

Para obtener información general de hello reciclaje de proceso, consulte [volver a entrenar un modelo de aprendizaje automático](machine-learning-retrain-machine-learning-model.md).

Si desea que toostart con el contenido existente nuevo administrador de recursos de Azure basada en servicio web, consulte [entrenar el modelo de un servicio web de predicción existente](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Crear un experimento de entrenamiento
En este ejemplo, usará "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" de ejemplos de aprendizaje automático de Microsoft Azure Hola. 

experimento de Hola toocreate:

1. Inicie sesión en tooMicrosoft estudio de aprendizaje automático de Azure. 
2. En hello esquina inferior derecha del panel de hello, haga clic en **nuevo**.
3. En Microsoft Samples hello, seleccione 5 de ejemplo.
4. experimento de hello toorename, en parte superior de hello del lienzo del experimento de hello, seleccione el nombre de experimento de Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult".
5. Escriba Census Model (Modelo de censo).
6. En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.
7. Haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Retraining Web Service** (Servicio web de reentrenamiento). 

siguiente Hello muestra experimento inicial Hola.
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Creación de un experimento predictivo y publicación como servicio web
A continuación creará un experimento predicativo.

1. En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **predictivo servicio Web**. Esto ahorra modelo Hola como un modelo entrenado y agrega módulos de entrada y salida del servicio web. 
2. Haga clic en **Ejecutar**. 
3. Después de experimento Hola ha terminado de ejecutarse, haga clic en **implementar servicio Web [estándar]** o **implementar [New] servicio Web**.

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Implementar Hola experimento de entrenamiento como un servicio web de aprendizaje
modelo de aprendizaje de hello tooretrain, debe implementar experimento de entrenamiento de Hola que creó como un servicio web de Retraining. Este servicio web necesita un *resultado del servicio Web* módulo conectado toohello  *[entrenar modelo] [ train-model]*  toobe tooproduce capaz de nuevo, el módulo modelos entrenados.

1. experimento de entrenamiento de tooreturn toohello, haga clic en el icono de experimentos hello en el panel izquierdo de hello, haga clic en el experimento Hola denominado modelo del censo.  
2. En el cuadro de búsqueda de elementos de experimento de búsqueda de hello, tipo de servicio web. 
3. Arrastre un *proporcionados por el servicio Web* módulo en hello experimentar lienzo y conectar su salida toohello *limpiar datos que faltan* módulo.  Esto garantiza que se procesan los datos reconversión Hola de igual manera que los datos de entrenamiento original.
4. Arrastre dos *salida del servicio web* módulos en hello experimentar lienzo. Conecte la salida de hello de hello *entrenar modelo* salida de hello y tooone del módulo de hello *evaluar modelo* módulo toohello otros. Hola resultado del servicio web para **entrenar modelo** nos da entrenado nueva Hola. Hola salida adjunta demasiado**evaluar modelo** devuelve ese módulo de salida de la, que es resultados de rendimiento de Hola.
5. Haga clic en **Ejecutar**. 

A continuación debe implementar Hola experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de la evaluación de modelo. tooaccomplish esto, el siguiente conjunto de acciones dependen de si está trabajando con un servicio de web estándar o un servicio web nuevo.  

**Servicio web clásico**

En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **implementar servicio Web [estándar]**. Servicio Web de Hola **panel** se muestra con la página de Ayuda de hello API hello y clave de API para la ejecución por lotes. Hola solo método de ejecución por lotes puede usarse para crear modelos entrenados.

**Servicio web nuevo**

En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **implementar [New] servicio Web**. portal de servicios Web de aprendizaje de máquina de Azure de Web Service Hola abre toohello implementar página al servicio web. Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**. Hola solo método de ejecución por lotes puede utilizarse para crear modelos entrenados

En cualquier caso, después de experimento tiene en ejecución completada, flujo de trabajo resultante Hola debe ser como sigue:

![Flujo de trabajo resultante después de la ejecución.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Volver a entrenar el modelo de Hola con datos nuevos mediante BES
En este ejemplo, está usando C# toocreate Hola reciclaje de aplicación. También sirve Hola Python o R ejemplo código tooaccomplish esta tarea.

toocall Hola API de reciclaje:

1. Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.
2. Inicie sesión en toohello portal de servicio Web de aprendizaje de máquina.
3. Si está trabajando con un servicio web clásico, haga clic en **Classic Web Services**(Servicios web clásicos).
   1. Haga clic en servicio web de Hola que está trabajando.
   2. Haga clic en el punto de conexión de hello predeterminado.
   3. Haga clic en **Consume**(Consumo).
   4. En parte inferior de Hola de hello **Consume** página Hola **código de ejemplo** sección, haga clic en **por lotes**.
   5. Continuar toostep 5 de este procedimiento.
4. Si está trabajando con un servicio web nuevo, haga clic en **Servicios web**.
   1. Haga clic en servicio web de Hola que está trabajando.
   2. Haga clic en **Consume**(Consumo).
   3. En parte inferior de Hola de hello Consume la página hello **código de ejemplo** sección, haga clic en **por lotes**.
5. Copiar código C# ejemplo de Hola para la ejecución por lotes y péguelo en el archivo Program.cs de hello, asegurándose de que el espacio de nombres de hello permanece intacto.

Agregar paquete de Nuget hello Microsoft.AspNet.WebApi.Client tal como se especifica en los comentarios de Hola. tooadd Hola referencia tooMicrosoft.WindowsAzure.Storage.dll, primero tendrá que biblioteca de cliente hello tooinstall para servicios de almacenamiento de Microsoft Azure. Para obtener más información, vea [Servicios de almacenamiento de Windows](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Actualizar la declaración de hello apikey
Busque hello **apikey** declaración.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Hola **información básica de consumo** sección de hello **Consume** página, busque la clave principal de Hola y cópielo toohello **apikey** declaración.

### <a name="update-hello-azure-storage-information"></a>Actualizar la información de almacenamiento de Azure Hola
código de ejemplo BES Hola carga un archivo desde un almacenamiento de tooAzure de unidad local (por ejemplo "C:\temp\CensusIpnput.csv"), lo procesa y escribe Hola resultados atrás tooAzure almacenamiento.  

tooaccomplish esta tarea, debe recuperar la información de nombre, la clave y el contenedor de la cuenta del almacenamiento hello para la cuenta de almacenamiento del portal de Azure clásico de Hola y actualización de hello correspondientes valores en el código de hello. 

1. Inicie sesión en el portal de Azure clásico toohello.
2. En la columna de navegación izquierdo de hello, haga clic en **almacenamiento**.
3. En lista de Hola de cuentas de almacenamiento, seleccione uno toostore Hola volver a entrenar modelo.
4. En la parte inferior de Hola de página de hello, haga clic en **administrar claves de acceso**.
5. Copie y guarde hello **clave de acceso principal** y cuadro de diálogo Cerrar Hola. 
6. En la parte superior de Hola de página de hello, haga clic en **contenedores**.
7. Seleccione un contenedor existente o cree uno nuevo y guarde el nombre de Hola.

Busque hello *StorageAccountName*, *StorageAccountKey*, y *StorageContainerName* Hola a declaraciones y actualizar valores de hello que guardó en el portal de Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

También debe asegurarse de archivo de entrada de hello está disponible en la ubicación de Hola que especifique en el código de hello. 

### <a name="specify-hello-output-location"></a>Especifique la ubicación de salida de hello
Al especificar la ubicación de salida de hello en hello la carga de solicitudes, Hola extensión del archivo de hello especificado en *RelativeLocation* debe especificarse como ilearner. 

Vea el siguiente ejemplo de Hola:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> nombres de Hola de sus ubicaciones de salida pueden ser diferentes de hello los en este tutorial basados en el orden de hello en el que se ha agregado módulos de salida de hello web service. Puesto que se configura este experimento de entrenamiento con dos salidas, resultados de hello incluyen información de ubicación de almacenamiento para ambos.  
> 
> 

![Salida de reentrenamiento][6]

Diagrama 4: Salida de entrenamiento.

## <a name="evaluate-hello-retraining-results"></a>Evaluar los resultados de reciclaje de Hola
Cuando se ejecuta la aplicación hello, salida de hello incluye la dirección URL de Hola y tooaccess necesarios de token de SAS Hola resultados de la evaluación.

Puede ver los resultados de rendimiento de Hola de hello volver a entrenar modelo mediante la combinación de hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello unos resultados para *output2* (como se muestra en hello anterior reciclaje imagen de salida) y pegar la dirección URL completa de hello en la barra de direcciones del explorador de Hola.  

Examine Hola resultados toodetermine si Hola recién entrenado realiza lo suficientemente bien hello tooreplace uno existente.

Hola copia *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de resultados de la salida de hello, utilizará durante Hola reciclaje de proceso.

## <a name="next-steps"></a>Pasos siguientes
Si ha implementado el servicio web de predicción de hello haciendo clic en **implementar servicio Web [estándar]**, consulte [entrenar el modelo de servicio web clásico](machine-learning-retrain-a-classic-web-service.md).

Si ha implementado el servicio web de predicción de hello haciendo clic en **implementar [New] servicio Web**, consulte [volver a entrenar un nuevo servicio web mediante los cmdlets de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
