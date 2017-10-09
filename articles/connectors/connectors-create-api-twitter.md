---
title: "aaaLearn cómo toouse Hola conector de Twitter en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de Twitter con parámetros de la API de REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Empezar a trabajar con el conector de Twitter de Hola
Con el conector de Twitter de hello hacer lo siguiente:

* Publicar y obtener tweets
* Acceder a escalas de tiempo, amigos y seguidores
* Realice cualquiera de hello otras acciones y desencadenadores que se describe a continuación  

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Conectar tooTwitter
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio. Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.  

### <a name="create-a-connection-tootwitter"></a>Crear una conexión tooTwitter
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Uso de un desencadenador de Twitter
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

En este ejemplo, le mostrará cómo hello toouse **cuando se registra un nuevo tweet** desencadena toosearch para #Seattle y, si se encuentra #Seattle, actualizar un archivo en Dropbox con texto hello tweet Hola. En un ejemplo de la empresa, podría buscar Hola nombre de su empresa y actualizar una base de datos SQL con texto hello tweet Hola.

1. Escriba *twitter* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **Twitter - cuando se registra un nuevo tweet** desencadenador   
   ![Imagen de desencadenador de Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Escriba *#Seattle* en hello **texto de búsqueda** control  
   ![Imagen de desencadenador de Twitter 2](./media/connectors-create-api-twitter/trigger-2.png) 

En este punto, la aplicación lógica se ha configurado con un desencadenador que se iniciará una ejecución del programa Hola a otros desencadenadores y acciones de flujo de trabajo de Hola. 

> [!NOTE]
> Para que una toobe de aplicación lógica funcional, debe contener al menos un desencadenador y una acción. Siga los pasos de Hola Hola siguiente sección tooadd una acción.  
> 
> 

## <a name="add-a-condition"></a>Agregar una condición
Puesto que sólo estamos interesados en tweets de los usuarios con más de 50 usuarios, una condición que se confirma el número de Hola de seguidores se debe agregar primero toohello aplicación de lógica.  

1. Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando #Seattle se encuentra en un tweet nueva  
   ![Imagen de acción de Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Seleccione hello **agregar una condición** vínculo.  
   ![Imagen de condición de Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Se abrirá hello **condición** control donde puede comprobar las condiciones como *es igual a*, *es menor que*, *es mayor que*, *contiene*, etcetera.  
   ![Imagen de condición de Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Seleccione hello **elegir un valor** control.  
   En este control, puede seleccionar una o varias de las propiedades de Hola de las acciones anteriores o los desencadenadores como valor de hello cuya condición será evaluada tootrue o false.
   ![Imagen de condición de Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Seleccione hello **...**  tooexpand lista de Hola de propiedades para que pueda ver todas las propiedades de Hola que están disponibles.        
   ![Imagen de condición de Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Seleccione hello **recuento seguidores** propiedad.    
   ![Imagen de condición de Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Tenga en cuenta seguidores de hello propiedad count es ahora en el control de valores de hello.    
   ![Imagen de condición de Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Seleccione **es mayor que** desde la lista de operadores de Hola.    
   ![Imagen de condición de Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Escriba 50 como Hola operando para hello *es mayor que* operador.  
   Ahora se agrega la condición de Hola. Guardar su trabajo con hello **guardar** vínculo en el menú de hello anterior.    
   ![Imagen de condición de Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Uso de una acción de Twitter
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Ahora que ha agregado un desencadenador, siga estas tooadd pasos una acción que se va a registrar un nuevo tweet con contenido de Hola de tweets de hello encontrados por el desencadenador de Hola. Para los fines de Hola de este tutorial se expondrá solo tweets de los usuarios con más de 50 seguidores.  

En el paso siguiente de hello, agregará una acción de Twitter que registrará un tweet usar algunas de las propiedades de Hola de cada tweet que se ha publicado por un usuario que tenga más de 50 seguidores.  

1. Seleccione **Add an action**(Agregar una acción). Esto abre el control de búsqueda de Hola donde puede buscar otras acciones y desencadenadores.  
   ![Imagen de condición de Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Escriba *twitter* en el cuadro de búsqueda de hello, a continuación, seleccione hello **de Twitter: registrar un tweet** acción. Se abrirá hello **registrar un tweet** control donde se incluirá todos los detalles de tweet Hola expuesta.      
   ![Imagen de acción de Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Seleccione hello **Tweet texto** control. Todos los resultados de las acciones anteriores y los desencadenadores de aplicación lógica de hello están visibles. Puede seleccionar cualquiera de ellos y usarlas como parte del texto de tweet Hola de nuevo tweet de Hola.     
   ![Imagen de acción de Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Seleccione **Nombre de usuario**.   
5. Escriba *dice:* Hola tweet control de texto. Hágalo justo después del nombre de usuario.  
6. Seleccione *Tweet text (Texto del tweet)*.       
   ![Imagen de acción de Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Guarde el trabajo y enviar un tweet con hello #Seattle hashtag tooactivate el flujo de trabajo.  


## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md)

