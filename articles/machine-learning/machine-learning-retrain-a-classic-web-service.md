---
title: "aaaRetrain un servicio web de clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically volver a entrenar un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Reentrenamiento de un servicio web clásico
Hola predictivo servicio Web implementa es predeterminado Hola la puntuación del punto de conexión. Puntos de conexión predeterminados se mantienen sincronizada con hello originales de entrenamiento y puntuación experimentos y, por tanto, hello entrenado para el punto de conexión de hello predeterminado no se puede reemplazar. servicio web de tooretrain hello, debe agregar un nuevo servicio web de toohello de punto de conexión. 

## <a name="prerequisites"></a>Requisitos previos
Debe haber configurado un experimento de entrenamiento y un experimento predictivo tal como se muestra en los [modelos de reciclaje de Machine Learning mediante programación](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> experimento predictivo Hola debe implementarse como un servicio web de aprendizaje de automático de clásico. 
> 
> 

Para obtener más información sobre la implementación de servicios web, vea el artículo sobre [implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Adición de un nuevo punto de conexión
Hola predictivo servicio Web que ha implementado contiene un punto de conexión que se mantiene en sincronización con entrenamiento original de Hola y puntuación entrenado de experimentos de puntuación predeterminado. tooupdate el servicio web, toowith un nuevo modelo entrenado, debe crear un nuevo extremo de puntuación. 

un nuevo extremo de puntuación, en hello predictivo servicio Web que se pueden actualizar con entrenado Hola toocreate:

> [!NOTE]
> Asegúrese de que está agregando Hola extremo toohello predictivo servicio Web, servicio Web de aprendizaje y no Hola. Si ha implementado correctamente un servicio web predictivo y otro de entrenamiento, debería ver dos servicios web independientes. Hola predictivo servicio Web debe terminar con "[exp predictiva.]".
> 
> 

Hay tres formas en que puede agregar un nuevo servicio web de tooa de punto de conexión:

1. De manera programática
2. Usar el portal de servicios Web de Microsoft Azure de Hola
3. Usar hello portal de Azure clásico

### <a name="programmatically-add-an-endpoint"></a>Incorporación de un punto de conexión mediante programación
Puede agregar extremos de puntuación mediante código de ejemplo de Hola proporcionado en este [repositorio de github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Usar Hola servicios Web de Microsoft Azure portal tooadd un punto de conexión
1. En estudio de aprendizaje automático, en la columna de navegación izquierdo de hello, haga clic en servicios Web.
2. En hello parte inferior del panel de servicio de hello web, haga clic en **vista previa de los puntos de conexión de administrar**.
3. Haga clic en **Agregar**.
4. Escriba un nombre y una descripción para el nuevo punto de conexión de Hola. Seleccione el nivel de registro de hello y si los datos de ejemplo está habilitado. Para más información sobre los registros, vea [Habilitar el registro para los servicios web de Aprendizaje automático](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Usar hello tooadd portal clásico un punto de conexión de Azure
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el menú de la izquierda hello, haga clic en **aprendizaje automático**.
3. En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.
4. En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).
5. En la parte inferior de Hola de página de hello, haga clic en **Agregar extremo**. Para más información sobre la incorporación de puntos de conexión, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Hola de actualización agrega entrenado del punto de conexión
proceso de reconversión de hello toocomplete, debe actualizar entrenado Hola de hello nuevo punto de conexión que agregó.

* Si ha agregado Hola nuevo punto de conexión mediante el portal de Azure clásico hello, puede haga clic en nombre de hello nuevo del punto de conexión en el portal de Hola y luego Hola **UpdateResource** tooget dirección URL de hello necesitaría modelo tooupdate Hola del punto de conexión del vínculo.
* Si ha agregado el punto de conexión de hello mediante código de ejemplo de Hola, esta información incluye la ubicación de dirección URL de la Ayuda de hello identificado por hello *HelpLocationURL* valor de salida de hello.

dirección URL de la ruta de acceso de hello del tooretrieve:

1. Copie y pegue la dirección URL de hello en el explorador.
2. Haga clic en el vínculo del recurso de actualización de Hola.
3. Copiar dirección URL de POST de solicitud de revisión de Hola Hola. Por ejemplo:
   
     PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

Ahora puede usar hello tooupdate Hola entrenado que la puntuación del punto de conexión que creó anteriormente.

Hola siguiendo el ejemplo de código muestra cómo hello toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*y el punto de conexión de dirección URL PATCH tooupdate Hola.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Hola *apiKey* hello y *endpointUrl* de llamada de hello puede obtenerse de panel de punto de conexión.

Hola valo hello *nombre* parámetro en *recursos* debe Hola de coincidencia de nombre de recurso de hello Guardar modelo entrenado en experimento predictivo Hola. Hola tooget nombre de recurso:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el menú de la izquierda hello, haga clic en **aprendizaje automático**.
3. En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.
4. En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).
5. Haga clic en nuevo extremo de Hola que agregó.
6. En el panel de punto de conexión de hello, haga clic en **recurso de actualización**.
7. En la página de documentación de API de recursos de actualización de hello para el servicio web de hello, puede buscar hello **nombre de recurso** en **recursos actualizables**.

Si el token SAS expira antes de que termine de actualizar el punto de conexión de hello, debe realizar una operación GET con el Id. de trabajo de hello tooobtain un nuevo token.

Cuando se ejecutó correctamente el código de hello, nuevo punto de conexión de hello debe empezar a utilizar Hola volver a entrenar modelo en 30 segundos aproximadamente.

## <a name="summary"></a>Resumen
Usar Hola reciclaje API, puede actualizar entrenado Hola de un servicio Web predictivos que permite escenarios como:

* Reentrenamiento de modelos periódicos con nuevos datos.
* Distribución de un modelo toocustomers con el objetivo de Hola de lo que permite volver a entrenar modelo hello mediante sus propios datos.

## <a name="next-steps"></a>Pasos siguientes
[Solución de problemas de hello reciclaje de un servicio web clásico de aprendizaje automático de Azure](machine-learning-troubleshooting-retraining-models.md)

