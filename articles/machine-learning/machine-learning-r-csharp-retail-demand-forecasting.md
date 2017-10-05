---
title: "(obsoleto) Previsión: ETS + STL - Azure | Microsoft Docs"
description: "(obsoleto) Previsión: ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a575af931a41b7a55eb2102f3553640a16099146
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>(obsoleto) Previsión: ETS + STL

> [!NOTE]
> Microsoft DataMarket está en proceso de retirada y esta API está en desuso. 
> 
> Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com). Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).

Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implementa la descomposición de tendencias estacionales (STL) y el modelo de suavizado exponencial (ETS) para generar previsiones basadas en datos históricos facilitados por el usuario. ¿Aumentará la demanda de un producto específico este año? ¿Puedo prever las ventas de productos para la temporada navideña, a fin de poder planear el inventario con eficacia? Los modelos de previsión suelen abordar estas cuestiones. Conforme a los datos anteriores, estos modelos examinan las tendencias ocultas y la estacionalidad para prever futuras tendencias. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
Este servicio acepta 4 argumentos y calcula las previsiones.
Los argumentos de entrada son:

* Frecuencia: indica la frecuencia de los datos sin procesar (diaria/semanal/mensual/trimestral/anual)
* Horizonte: intervalo de tiempo de previsión del futuro.
* Fechas: permite agregar los nuevos datos de la serie temporal para el tiempo.
* Valor: permite agregar los nuevos valores de datos de series temporales.

La salida del servicio se corresponde con los valores de previsión calculados.

La entrada de ejemplo podría ser: 

* Frecuencia: 12
* Horizonte: 12
* Fecha: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014
* Valor: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET. 
> 
> 

Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)se puede ver una aplicación de ejemplo).

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
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.
> 
> 

Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco. Se cargaron datos de entrada de muestra con un esquema de datos predefinido. Vinculado al esquema de datos hay un módulo [Ejecutar scripts R][execute-r-script] que genera el modelo de previsión STL y ETS mediante las funciones "auto.arima" y "previsión" de R. 

### <a name="experiment-flow"></a>Flujo de experimento:
![Flujo de experimento][2]

#### <a name="module-1"></a>Módulo 1:
    # Add in the CSV file with the data in the format shown below 
![Datos de ejemplo][3]    

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

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Limitaciones
Este es un ejemplo muy sencillo de previsión de ETS+STL. Como puede verse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio asume que todas las variables son valores continuos/positivos y la frecuencia debe ser un entero mayor que 1. La longitud de los vectores de fecha y valor debe ser la misma, y la longitud de la serie temporal debe ser superior a 2*frecuencia. La variable de fecha debe respetar el formato "dd/mm/aaaa".

## <a name="faq"></a>P+F
Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

