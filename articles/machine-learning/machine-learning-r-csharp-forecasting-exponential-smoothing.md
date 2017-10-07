---
title: aaa(deprecated) Forecasting - Suavizado exponencial - Azure | Documentos de Microsoft
description: "(obsoleto) Servicio web: previsión - suavizado exponencial"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a>(obsoleto) Previsión: suavizado exponencial

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/ets) implementa Hola Suavizado exponencial predicciones de tooproduce modelo (ETS) basadas en datos históricos de hello proporcionados por usuario de Hola. ¿Hola a petición para un aumento de productos específica este año? ¿Predecir Mis ventas de producto para hello Navidad, para que puedo planear eficazmente mi inventario? Modelos de predicción son tooaddress apt esas preguntas. Dados hello más allá de los datos, estos modelos examinan tendencias ocultas y las tendencias futuras estacionalidad toopredict.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
Este servicio acepta 4 argumentos y calcula las previsiones ETS Hola.
argumentos de entrada de Hello son:

* Frecuencia: indica la frecuencia de Hola de datos sin procesar de hello (diaria/semanal/mensual o trimestral/anual).
* Horizonte: intervalo de tiempo de previsión del futuro.
* Fecha: agregar datos de la serie temporal de la nueva Hola por vez.
* Valor: agregar en valores de datos en la serie de tiempo de hello nueva.

salida de Hello del servicio de hello es Hola calcula valores pronosticados.

La entrada de ejemplo podría ser: 

* Frecuencia: 12
* Horizonte: 12
* Fecha: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014
* Valor: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.
> 
> 

Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco. Se cargaron datos de entrada de muestra con un esquema de datos predefinido. Esquema de datos de toohello vinculado es un [ejecutar Script de R] [ execute-r-script] módulo que genera Hola ETS previsión modelo mediante el uso de funciones 'ets' y 'previsión' de R. 

![Flujo de experimento][2]

#### <a name="module-1"></a>Módulo 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Ejemplo de datos][3]    

#### <a name="module-2"></a>Módulo 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>Limitaciones
Este es un ejemplo muy sencillo de previsión de ETS. Como se puede ver desde el código de ejemplo de Hola anterior, realizar capturas de errores no se implementan y servicio Hola se supone que todas las variables de hello son valores continuos/positive y frecuencia de hello debe ser un entero mayor que 1. longitud de Hola de vectores de valor de fecha y de Hola se debería Hola mismo. variable de fecha Hola debe respetar toohello formato "mm/dd/aaaa'.

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

