---
title: "Recomendaciones de Machine Learning: integración con JavaScript | Microsoft Docs"
description: "Recomendaciones de Azure Machine Learning: integración con JavaScript (documentación)"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Recomendaciones de Aprendizaje automático de Azure: Integración con JavaScript
> [!NOTE]
> Debe empezar a utilizar el servicio Cognitive Services de la API de Recomendaciones en lugar de esta versión. El servicio Cognitive Services de Recomendaciones va a sustituir a este servicio y todas las características nuevas se desarrollarán en esta nueva versión. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
> Obtenga más información sobre cómo [migrar al nuevo servicio Cognitive Services](http://aka.ms/recomigrate)
> 
> 

Este documento describe cómo integrar su sitio mediante JavaScript. El código JavaScript le permite enviar eventos de adquisición de datos y consumir recomendaciones una vez que se crea un modelo de recomendación. Todas las operaciones que se realizan a través de JS se pueden realizar también desde el servidor.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Información general
La integración de su sitio con recomendaciones de Aprendizaje automático de Azure consta de 2 fases:

1. Enviar eventos a las recomendaciones de Aprendizaje automático de Azure. Esto le permitirá crear un modelo de recomendación.
2. Use las recomendaciones. Una vez generado el modelo, puede utilizar las recomendaciones. (Este documento no explica cómo crear un modelo; lea la Guía de inicio rápido para obtener más información acerca de cómo).

<ins>Fase I</ins>

En la primera fase, insertará en sus páginas html una pequeña biblioteca de JavaScript que permita a la página enviar eventos a medida que se producen en la página html en servidores de recomendaciones de Aprendizaje automático de Azure (a través del mercado de datos):

![Dibujo1][1]

<ins>Fase II</ins>

En la segunda fase, si desea mostrar las recomendaciones en la página, seleccione una de las siguientes opciones:

1. Su servidor (en la fase de representación de la página) llama al servidor de recomendaciones de Aprendizaje automático de Azure (a través de mercado de datos) para obtener recomendaciones. Los resultados incluyen una lista de id. de elementos. El servidor necesita enriquecer los resultados con los elementos de metadatos (por ejemplo, imágenes, descripción) y enviar la página creada al explorador.

![Dibujo2][2]

2. La otra opción es utilizar el archivo de JavaScript pequeño de la fase uno para obtener una lista de elementos recomendados. Los datos recibidos son más simples que los que aparecen en la primera opción.

![Dibujo3][3]

## <a name="2-prerequisites"></a>2. Requisitos previos
1. Cree un modelo nuevo mediante las API. Vea la Guía de inicio rápido para saber cómo hacerlo.
2. Codifique &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; mediante base64. (Esto se utilizará para la autenticación básica para permitir que el código JS llame a las API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Envíe eventos de adquisición de datos con JavaScript.
Los siguientes pasos permiten enviar eventos:

1. Incluya la biblioteca de JQuery en su código. Puede descargarlo desde nuget en la siguiente dirección URL.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Incluya la biblioteca de recomendaciones de Java Script que encontrará en la siguiente dirección URL: http://aka.ms/RecoJSLib1.
3. Inicialice la biblioteca de recomendaciones de Aprendizaje automático de Azure con los parámetros adecuados.
   
     <script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Envíe el evento adecuado. Consulte la sección detallada a continuación respecto a todos los tipos de eventos (ejemplo de evento de clic)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitaciones y compatibilidad con exploradores
Esta es una implementación de referencia y se proporciona tal cual. Debe admitir todos los exploradores principales.

### <a name="32----type-of-events"></a>3.2.    Tipos de eventos
Hay cinco tipos de eventos que admite la biblioteca: hacer clic, clic de recomendación, agregar al carro de la compra , quitar del carro de la compra y comprar. Hay un evento adicional que se utiliza para establecer el contexto de usuario denominado Inicio de sesión.

#### <a name="321-click-event"></a>3.2.1. Evento de clic
Este evento se debe utilizar cada vez que un usuario hace clic en un elemento. Normalmente, cuando el usuario hace clic en un elemento, se abre una nueva página con los detalles de dicho elemento; en esta página, debería activarse este evento.

Parámetros:

* event (cadena, obligatorio) - “click”
* item (cadena, obligatorio) - Identificador único del elemento
* itemName (cadena, opcional) - El nombre del elemento
* itemDescription (cadena, opcional) - Descripción del elemento
* itemCategory (cadena, opcional) - La categoría del elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

O con datos opcionales:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Ejemplo de Recommendation Click:
Este evento se debe utilizar cada vez que un usuario hace clic en un elemento que se recibió de las recomendaciones de Aprendizaje automático de Azure como un elemento recomendado. Normalmente, cuando el usuario hace clic en un elemento, se abre una nueva página con los detalles de dicho elemento; en esta página, debería activarse este evento.

Parámetros:

* event (cadena, obligatorio) - “recommendationclick”
* item (cadena, obligatorio) - Identificador único del elemento
* itemName (cadena, opcional) - El nombre del elemento
* itemDescription (cadena, opcional) - Descripción del elemento
* itemCategory (cadena, opcional) - La categoría del elemento
* seeds (matriz de cadena, opcional) - Los valores de inicialización que generaron la consulta de recomendación.
* recoList (matriz de cadena, opcional) - El resultado de la solicitud de recomendación que generó el elemento en el que se hizo clic.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

O con datos opcionales:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Agregar eventos de carro de la compra
Este evento se debe usar cuando el usuario agrega un elemento al carro de la compra.
Parámetros:

* event (cadena, obligatorio) - "addshopcart"
* item (cadena, obligatorio) - Identificador único del elemento
* itemName (cadena, opcional) - El nombre del elemento
* itemDescription (cadena, opcional) - Descripción del elemento
* itemCategory (cadena, opcional) - La categoría del elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Quitar eventos de carro de la compra
Este evento se debe usar cuando el usuario quita un elemento del carro de la compra.

Parámetros:

* event (cadena, obligatorio) - "removeshopcart"
* item (cadena, obligatorio) - Identificador único del elemento
* itemName (cadena, opcional) - El nombre del elemento
* itemDescription (cadena, opcional) - Descripción del elemento
* itemCategory (cadena, opcional) - La categoría del elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Evento de compra
Este evento se debe usar cuando el usuario ha comprado su carro de la compra.

Parámetros:

* event (cadena) - "purchase"
* items ( Purchased[] ) - Matriz con una entrada por cada elemento comprado.<br><br>
  Formato de elemento comprado:
  * item (cadena) - Identificador único del elemento
  * count (entero o cadena) - Número de elementos que se compraron.
  * price (flotante o cadena) - Campo opcional; precio del elemento.

El ejemplo siguiente muestra la compra de 3 elementos (33, 34, 35), dos con todos los campos (elemento, cantidad, precio) y uno (elemento 34) sin precio.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Evento de inicio de sesión de usuario
La biblioteca de eventos de recomendaciones de Aprendizaje automático de Azure crea y utiliza una cookie para identificar los eventos que provienen del mismo explorador. Para mejorar los resultados del modelo, las recomendaciones de Aprendizaje automático de Azure permiten establecer una identificación única de usuario que omitirá el uso de cookies.

Este evento se debe utilizar después del inicio de sesión de usuario en su sitio.

Parámetros:

* event (cadena) - "userlogin"
* user (cadena) - Identificación único del usuario.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Consumir recomendaciones a través de JavaScript
El código que consume la recomendación se activa por algunos eventos de JavaScript en la página web del cliente. La respuesta de recomendación incluye los identificadores de elementos recomendados, sus nombres y sus clasificaciones. Es preferible utilizar esta opción solo para una visualización de la lista de los elementos recomendados: debe realizarse un control más complejo (por ejemplo, para agregar los metadatos del elemento) en la integración del lado servidor.

### <a name="41-consume-recommendations"></a>4.1 Recomendaciones de uso
Para consumir recomendaciones, deberá incluir las bibliotecas JavaScript requeridas en la página y llamar a AzureMLRecommendationsStart. Consulte la sección 2.

Para consumir recomendaciones para uno o varios elementos, debe llamar a un método denominado: AzureMLRecommendationsGetI2IRecommendation.

Parámetros:

* items (matriz de cadenas) - Uno o varios elementos para los que obtener recomendaciones. Si consume una compilación Fbt, aquí solo puede establecer un elemento.
* numberOfResults (entero) - Número de resultados requeridos.
* includeMetadata (booleano, opcional) - Si se establece en ‘true’ indica que el campo de metadatos se debe rellenar en el resultado.
* Función de procesamiento - Una función que controlará las recomendaciones devueltas. Los datos se devuelven como una matriz de:
  * item - Identificador único del elemento
  * name - Nombre del elemento (si existe en el catálogo)
  * rating - Clasificación de recomendación
  * metadata - Una cadena que representa los metadatos del elemento

Ejemplo: El siguiente código solicita 8 recomendaciones para el elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (y al no especificar includeMetadata, se indica implícitamente que no se requieren metadatos), y luego concatena los resultados en un búfer.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
