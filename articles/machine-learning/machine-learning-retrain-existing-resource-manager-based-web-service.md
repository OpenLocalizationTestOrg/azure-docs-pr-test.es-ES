---
title: aaaRetrain predictivo existente servicio web | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooretrain un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Reciclaje de un servicio web predictivo existente
Este documento describe Hola reciclaje de proceso para hello siguiendo el escenario:

* Dispone de un experimento de entrenamiento y un experimento predictivo que se ha implementado como un servicio web de operaciones.
* Tiene nuevos datos que desea que su tooperform de toouse de servicio web de predicción su puntuación.

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

A partir de su servicio web existente y los experimentos, necesita toofollow estos pasos:

1. Actualizar modelo Hola.
   1. Modifique la tooallow de experimento de entrenamiento para web servicio entradas y salidas.
   2. Implementar Hola experimento de entrenamiento como un servicio web reconversión.
   3. Utilizar modelo de Hola de tooretrain de servicio de ejecución de lotes (BES) del experimento de entrenamiento de Hola.
2. Utilice el experimento de predicción de hello Azure Machine Learning PowerShell cmdlets tooupdate Hola.
   1. Inicie sesión en tooyour cuenta de administrador de recursos de Azure.
   2. Obtener la definición de servicio web de Hola.
   3. Exportar la definición del servicio web hello como JSON.
   4. Actualizar el blob de hello referencia toohello ilearner Hola JSON.
   5. Importar Hola JSON en una definición de servicio web.
   6. Actualizar el servicio web de hello con una nueva definición de servicio web.

## <a name="deploy-hello-training-experiment"></a>Implementar el experimento de entrenamiento de Hola
toodeploy Hola experimento de entrenamiento como un servicio web reconversión, debe agregar el modelo de toohello de entradas y salidas del servicio web. Conectando un *resultado del servicio Web* del experimento de módulo toohello  *[entrenar modelo] [ train-model]*  módulo, se habilita Hola experimento de entrenamiento tooproduce un nuevo modelo entrenado que puede usar en el experimento de predicción. Si tiene una *evaluar modelo* módulo, también puede adjuntar los resultados de evaluación de Hola de tooget en la salida del servicio web como salida.

tooupdate el experimento de entrenamiento:

1. Conectar un *entrada de servicio Web* datos tooyour del módulo de entrada (por ejemplo, un *limpiar datos que faltan* módulo). Normalmente, deseará tooensure que los datos de entrada se procesa en Hola de igual manera que los datos de entrenamiento original.
2. Conectar un *resultado del servicio Web* toohello salida del módulo de su *entrenar modelo* módulo.
3. Si tiene una *evaluar modelo* módulo y desea toooutput resultados de la evaluación de hello, conecte un *resultado del servicio Web* toohello salida del módulo de su *evaluar modelo* módulo.

Ejecute el experimento.

A continuación, debe implementar Hola experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de la evaluación de modelo.  

En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web**y, a continuación, seleccione **implementar [New] servicio Web**. Abre el portal de servicios Web de Azure Machine Learning Hello toohello **implementar el servicio de Web** página. Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**. Solo puede usar el método de ejecución por lotes de hello para la creación de modelos entrenados.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Volver a entrenar modelo de hello con nuevos datos utilizando BES
En este ejemplo, estamos usando C# toocreate Hola reciclaje de aplicación. También puede utilizar Python o R tooaccomplish de código de ejemplo de esta tarea.

toocall Hola reciclaje API:

1. Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.
2. Inicie sesión en toohello portal de servicios Web de aprendizaje de máquina.
3. Haga clic en el servicio web de Hola que está trabajando con.
4. Haga clic en **Consume**(Consumo).
5. En parte inferior de Hola de hello **Consume** página Hola **código de ejemplo** sección, haga clic en **por lotes**.
6. Copiar código C# ejemplo de Hola para la ejecución por lotes y péguelo en el archivo Program.cs de Hola. Asegúrese de que ese espacio de nombres Hola permanece intacta.

Agregar paquete de NuGet hello Microsoft.AspNet.WebApi.Client, tal como se especifica en los comentarios de Hola. tooadd Hola referencia tooMicrosoft.WindowsAzure.Storage.dll, primero deberá hello tooinstall [biblioteca de cliente para servicios de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

captura de pantalla siguiente Hello muestra hello **Consume** página del portal de servicios Web de Azure Machine Learning Hola.

![Página Consumo][1]

### <a name="update-hello-apikey-declaration"></a>Actualizar la declaración de hello apikey
Busque hello **apikey** declaración:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Hola **información básica de consumo** sección de hello **Consume** página, busque la clave principal de Hola y cópielo toohello **apikey** declaración.

### <a name="update-hello-azure-storage-information"></a>Actualizar la información de almacenamiento de Azure Hola
código de ejemplo BES Hola carga un archivo desde un almacenamiento de tooAzure de unidad local (por ejemplo, "C:\temp\CensusIpnput.csv"), lo procesa y escribe Hola resultados atrás tooAzure almacenamiento.  

información de almacenamiento de Azure de tooupdate hello, debe recuperar la cuenta de almacenamiento de hello información de nombre, la clave y el contenedor de su cuenta de almacenamiento de hello portal de Azure clásico y, a continuación, actualización hello correspondi después de ejecutar el experimento, Hola resultante flujo de trabajo debería ser similar siguiente toohello:

![Flujo de trabajo resultante después de la ejecución][4]valores de NG en el código de hello.

1. Inicie sesión en toohello portal de Azure clásico.
2. En la columna de navegación izquierdo de hello, haga clic en **almacenamiento**.
3. En lista de Hola de cuentas de almacenamiento, seleccione uno toostore Hola volver a entrenar modelo.
4. En la parte inferior de Hola de página de hello, haga clic en **administrar claves de acceso**.
5. Copie y guarde hello **clave de acceso principal** y cuadro de diálogo Cerrar Hola.
6. En la parte superior de Hola de página de hello, haga clic en **contenedores**.
7. Seleccione un contenedor existente, o crear uno nuevo y guarde el nombre de Hola.

Busque hello *StorageAccountName*, *StorageAccountKey*, y *StorageContainerName* declaraciones y actualizar los valores de hello que guardó en el portal clásico de Hola .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

También debe asegurarse de que ese archivo de entrada de hello está disponible en la ubicación de Hola que especifique en el código de hello.

### <a name="specify-hello-output-location"></a>Especifique la ubicación de salida de hello
Cuando se especifica la ubicación de salida de hello en hello la carga de solicitudes, Hola extensión del archivo de Hola que se especifica en *RelativeLocation* debe especificarse como `ilearner`. Vea el siguiente ejemplo de Hola:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Hello aquí te mostramos un ejemplo de reciclaje de salida: ![reciclaje salida][6]

## <a name="evaluate-hello-retraining-results"></a>Evaluar Hola reciclaje resultados
Cuando se ejecuta la aplicación hello, resultado de hello incluye dirección URL de Hola y token de firmas de acceso compartido que se muestran resultados de evaluación de hello tooaccess necesarios.

Puede ver los resultados de rendimiento de Hola de hello volver a entrenar modelo mediante la combinación de hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello unos resultados para *output2* (como se muestra en hello anterior reciclaje imagen de salida) y pegue la dirección URL completa de hello en barra de direcciones del explorador de Hola.  

Examine Hola resultados toodetermine si Hola recién entrenado realiza lo suficientemente bien hello tooreplace uno existente.

Hola copia *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello mostrar los resultados.

## <a name="retrain-hello-web-service"></a>Entrenar el modelo de servicio web de Hola
Al entrenar el modelo de un servicio web nuevo, se actualiza hello web predictivo servicio definición tooreference Hola nuevo modelo entrenado. definición del servicio web Hello es una representación interna de entrenado Hola del servicio web de hello y no es modificable directamente. Asegúrese de que está recuperando definición del servicio web hello para el experimento de predicción y no el experimento de entrenamiento.

## <a name="sign-in-tooazure-resource-manager"></a>Inicie sesión en el Administrador de recursos tooAzure
Debe iniciar sesión en la cuenta de Azure desde dentro del entorno de PowerShell de hello tooyour mediante el uso de hello [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Obtener el objeto de definición de servicio Web de Hola
A continuación, obtener objeto de definición de servicio Web de Hola Hola llamada [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine el nombre de grupo de recursos de Hola de un servicio web existente, ejecute el cmdlet de Get-AzureRmMlWebService de hello sin ningún servicio web de parámetros toodisplay hello en su suscripción. Busque el servicio web de hello y, a continuación, examine su identificador de servicio web. nombre de Hola Hola del grupo de recursos es el cuarto elemento de hello en el identificador hello, justo después de hello *resourceGroups* elemento. En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

O bien, toodetermine Hola nombre grupo de recursos de un miembro de servicio web, inicie sesión en el portal de servicios Web de Azure Machine Learning toohello. Seleccione el servicio web de Hola. nombre del grupo de recursos de Hello es quinto elemento de Hola de hello URL del servicio web de hello, justo después de hello *resourceGroups* elemento. En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Exportar el objeto de definición de servicio Web de hello como JSON
definición de hello toomodify de hello de hello entrenado toouse recién entrena el modelo, primero debe usar hello [AzureRmMlWebService de exportación](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de cmdlet, archivo tooa formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Actualizar Hola referencia toohello ilearner blob
En los activos de hello, busque Hola [entrenado], actualización hello *uri* valor Hola *locationInfo* nodo con hello URI de blob de hello ilearner. Hello URI generado por la combinación de hello *BaseLocation* hello y *RelativeLocation* de salida de hello de hello llamada reconversión BES.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Importar Hola JSON en un objeto de definición de servicio Web
Debe usar hello [AzureRmMlWebService de importación](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hola modifica archivo JSON en un objeto de definición de servicio Web que se puede usar el experimento de predicative tooupdate Hola.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Actualizar el servicio web de Hola
Por último, utilice hello [AzureRmMlWebService actualización](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hola experimento de predicción.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
