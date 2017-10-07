---
title: aaa(deprecated) diferencia en proporciones prueba - Azure | Documentos de Microsoft
description: (obsoleto) Diferencia en la prueba de proporciones
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>(obsoleto) Diferencia en la prueba de proporciones

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

¿Las dos proporciones son diferentes desde el punto de vista estadístico? Suponga que un usuario desea toocompare dos películas toodetermine si una película tiene una proporción significativamente superior del 'le gusta' cuando compara toohello otro. Con un ejemplo de gran tamaño, podría haber una diferencia significativa estadísticamente entre las proporciones Hola 0,50 y 0,51. Con una pequeña muestra, que no haya suficiente toodetermine datos si estas proporciones son realmente diferentes. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/prop_test) lleva a cabo una prueba de la hipótesis de diferencia de hello en dos proporciones basadas en la entrada de usuario de número de Hola de operaciones correctas y Hola el número total de pruebas para los grupos de comparación de hello 2. En un escenario posible, este servicio web podría invocarse desde dentro de una aplicación de comparación de película, indicando que el usuario de hello si uno de películas de hello es 'gustó' con más frecuencia que Hola otro, en función de las clasificaciones de películas.

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
Este servicio acepta 4 argumentos y realiza una prueba hipotética de las proporciones.

argumentos de entrada de Hello son:

* Éxitos1: número de eventos de éxito del ejemplo 1.
* Éxitos2: número de eventos de éxito del ejemplo 2.
* Total1: tamaño de la muestra 1.
* Total2: tamaño de la muestra 2.

salida de Hello del servicio de hello es resultado de hello de hipótesis Hola probar junto con hello chi-square estadística, df, p-valor y proporción en los límites del ejemplo 1/2 y el intervalo de confianza.

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
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

En Azure Machine Learning, se creó un nuevo experimento en blanco con dos módulos [Ejecutar script R][execute-r-script]. En el primer módulo de hello esquema de datos de Hola se define, mientras que segundo módulo de hello utiliza comandos de prop.test de hello en pruebas de hipótesis de R tooperform Hola para 2 proporciones. 

### <a name="experiment-flow"></a>Flujo de experimento:
![Flujo de experimento][2]

#### <a name="module-1"></a>Módulo 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Módulo 2:
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>Limitaciones
Se trata de un ejemplo muy sencillo para probar las diferencias entre dos proporciones. Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y servicio Hola se da por supuesto que todas las variables de hello son continuas.

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

