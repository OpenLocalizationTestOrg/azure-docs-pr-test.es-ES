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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Recomendaciones de Aprendizaje automático de Azure: Integración con JavaScript
> [!NOTE]
> Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión. Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
> Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)
> 
> 

Este documento describir cómo toointegrate su sitio mediante JavaScript. Hola JavaScript permite toosend eventos de adquisición de datos y las recomendaciones de tooconsume una vez que se genera un modelo de recomendación. Todas las operaciones que se realizan a través de JS se pueden realizar también desde el servidor.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Información general
La integración de su sitio con recomendaciones de Aprendizaje automático de Azure consta de 2 fases:

1. Enviar eventos a las recomendaciones de Aprendizaje automático de Azure. Esto le permitirá toobuild un modelo de recomendación.
2. Utilizar las recomendaciones de Hola. Después de que se crea el modelo de hello pueden consumir las recomendaciones de Hola. (Este documento no explica cómo toobuild un modelo, leer Hola tooget de guía de inicio rápido para obtener más información acerca de cómo).

<ins>Fase I</ins>

Hola primera fase que se inserta en las páginas html de una pequeña biblioteca de JavaScript que permite Hola eventos toosend de página cuando se producen en la página html hello en servidores de recomendaciones de aprendizaje automático de Azure (a través del mercado de datos):

![Dibujo1][1]

<ins>Fase II</ins>

Hola segunda fase cuando desee tooshow recomendaciones de hello en página Hola selecciona una de hello siguientes opciones:

1. el servidor (en la fase de hello de la representación de página) llama a las recomendaciones de tooget de servidor de recomendaciones de aprendizaje automático de Azure (a través de mercado de datos). resultados de Hello incluyen una lista de Id. de elementos. El servidor necesita resultados de hello tooenrich con hello los elementos de metadatos (por ejemplo, imágenes, descripción) y enviar Hola creado página toohello explorador.

![Dibujo2][2]

2. hello otra opción es archivo JavaScript toouse Hola pequeño de fase uno tooget una simple lista de elementos recomendados. datos de Hello recibidos aquí están más simple de hello en la primera opción de Hola.

![Dibujo3][3]

## <a name="2-prerequisites"></a>2. Requisitos previos
1. Crear un modelo nuevo mediante las API de Hola. Consulte la Guía de inicio rápido de hello acerca de cómo toodo lo.
2. Codifique &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; mediante base64. (Esto se usará para hello autenticación básica tooenable Hola JS código toocall Hola API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Envíe eventos de adquisición de datos con JavaScript.
Hola pasos facilitar enviar eventos:

1. Incluya la biblioteca de JQuery en su código. Puede descargarlo de nuget en hello después de la dirección URL.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Incluir Hola biblioteca de secuencia de comandos de Java de recomendaciones de hello después de la dirección URL: http://aka.ms/RecoJSLib1
3. Inicializar la biblioteca de recomendaciones de aprendizaje automático de Azure con los parámetros adecuados de Hola.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Eventos de envío Hola apropiado. Consulte la sección detallada a continuación respecto a todos los tipos de eventos (ejemplo de evento de clic)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitaciones y compatibilidad con exploradores
Esta es una implementación de referencia y se proporciona tal cual. Debe admitir todos los exploradores principales.

### <a name="32----type-of-events"></a>3.2.    Tipos de eventos
Hay 5 tipos de eventos que admite la biblioteca de Hola: haga clic en, haga clic en la recomendación, agregar tooShop carro, quitar de carro de la tienda y compra. Hay un evento adicional que es el contexto de usuario de Hola tooset utilizados llamado inicio de sesión.

#### <a name="321-click-event"></a>3.2.1. Evento de clic
Este evento se debe utilizar cada vez que un usuario hace clic en un elemento. Normalmente cuando el usuario hace clic en un elemento se abre una nueva página en los detalles de artículo de hello; en esta página debe activarse este evento.

Parámetros:

* event (cadena, obligatorio) - “click”
* elemento (string, obligatorio): identificador único del elemento de Hola
* itemName (cadena, opcional) nombre de Hola de elemento de Hola
* Descripción de producto (string, opcional): descripción de Hola de elemento de Hola
* itemCategory (cadena, opcional) categoría de Hola de elemento de Hola
  
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
Este evento se debe utilizar cada vez que un usuario hace clic en un elemento que se recibió de las recomendaciones de Aprendizaje automático de Azure como un elemento recomendado. Normalmente cuando el usuario hace clic en un elemento se abre una nueva página en los detalles de artículo de hello; en esta página debe activarse este evento.

Parámetros:

* event (cadena, obligatorio) - “recommendationclick”
* elemento (string, obligatorio): identificador único del elemento de Hola
* itemName (cadena, opcional) nombre de Hola de elemento de Hola
* Descripción de producto (string, opcional): descripción de Hola de elemento de Hola
* itemCategory (cadena, opcional) categoría de Hola de elemento de Hola
* valores de inicialización (matriz de cadenas, opcional) - Hola inicializaciones que genera la consulta de la recomendación de Hola.
* recoList (matriz de cadenas, opcional) - Hola resultado de solicitud de recomendación de Hola que generó el elemento de Hola que se hizo clic.
  
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
Este evento debe usarse cuando el usuario de hello agrega un toohello elemento carro de la compra.
Parámetros:

* event (cadena, obligatorio) - "addshopcart"
* elemento (string, obligatorio): identificador único del elemento de Hola
* itemName (cadena, opcional) nombre de Hola de elemento de Hola
* Descripción de producto (string, opcional): descripción de Hola de elemento de Hola
* itemCategory (cadena, opcional) categoría de Hola de elemento de Hola
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Quitar eventos de carro de la compra
Este evento debe usarse cuando el usuario de hello quita un carro de la compra toohello elemento.

Parámetros:

* event (cadena, obligatorio) - "removeshopcart"
* elemento (string, obligatorio): identificador único del elemento de Hola
* itemName (cadena, opcional) nombre de Hola de elemento de Hola
* Descripción de producto (string, opcional): descripción de Hola de elemento de Hola
* itemCategory (cadena, opcional) categoría de Hola de elemento de Hola
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Evento de compra
Este evento debe usarse cuando el usuario de hello adquirió su carro de la compra.

Parámetros:

* event (cadena) - "purchase"
* items ( Purchased[] ) - Matriz con una entrada por cada elemento comprado.<br><br>
  Formato de elemento comprado:
  * elemento (cadena): identificador único del elemento de Hola.
  * count (entero o cadena) - Número de elementos que se compraron.
  * precio (float o cadena) - field opcional: Hola precio del elemento de Hola.

ejemplo de Hola siguiente muestra la compra de 3 elementos (33, 34, 35), dos con todos los campos rellena (elemento, recuento, precio) y otra (elemento 34) sin un precio.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Evento de inicio de sesión de usuario
Azure evento de recomendaciones de aprendizaje automático biblioteca crea y utiliza una cookie en los eventos de tooidentify de orden que proviene de Hola mismo explorador. Modelo de orden tooimprove Hola recomendaciones de aprendizaje automático de Azure de resultados permite tooset una identificación única de usuario que reemplazará el uso de cookies de Hola.

Este evento se debe utilizar después el sitio de tooyour de inicio de sesión de usuario de Hola.

Parámetros:

* event (cadena) - "userlogin"
* usuario (cadena) de identificación único del usuario de Hola.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Consumir recomendaciones a través de JavaScript
página Web del cliente de hello desencadenan código de Hello que consume la recomendación de Hola por algunos eventos de JavaScript. respuesta de la recomendación de Hello incluye Hola recomendadas identificadores de elementos, sus nombres y sus clasificaciones. Es mejor toouse esta opción solo para una visualización de la lista de hello recomendada elementos - más complejos de control (por ejemplo, para agregar metadatos de elemento de Hola) se debe realizar en la integración del lado servidor de Hola.

### <a name="41-consume-recommendations"></a>4.1 Recomendaciones de uso
recomendaciones de tooconsume que necesita tooinclude Hola requiere bibliotecas de JavaScript en la página y toocall AzureMLRecommendationsStart. Consulte la sección 2.

recomendaciones de tooconsume para uno o más elementos necesita toocall llama a un método: AzureMLRecommendationsGetI2IRecommendation.

Parámetros:

* Una o más elementos tooget recomendaciones para los elementos (matriz de cadenas). Si consume una compilación Fbt, aquí solo puede establecer un elemento.
* numberOfResults (entero) - Número de resultados requeridos.
* includeMetadata (un valor booleano, opcional) - si establece too'true' indica que se debe rellenar ese campo de metadatos de hello en el resultado de hello.
* Devuelve la función: una función que controlará las recomendaciones de Hola de procesamiento. Hola datos se devuelven como una matriz de:
  * item - Identificador único del elemento
  * name - Nombre del elemento (si existe en el catálogo)
  * rating - Clasificación de recomendación
  * metadatos: una cadena que representa los metadatos de Hola de elemento de Hola

Ejemplo: Hola después el código solicita 8 recomendaciones para el elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (y especificando no includeMetadata - implícitamente dice que no hay metadatos están necesario),, a continuación, concatenar los resultados de hello en un búfer.

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
