---
title: expresiones condicionales de motor de reglas de aaaAzure CDN | Documentos de Microsoft
description: "Documentación de referencia sobre las condiciones y características de coincidencia del motor de reglas de la red CDN de Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Expresiones condicionales del motor de reglas de la red CDN de Azure
Este tema enumeran las descripciones detalladas de hello expresiones condicionales del red de entrega de contenido (CDN) para Azure [motor de reglas de](cdn-rules-engine.md).

primera parte de una regla de Hello es hello expresión condicional.

Expresión condicional | Descripción
-----------------------|-------------
IF | Una expresión IF siempre es una parte de la primera instrucción de hello en una regla. Al igual que las demás expresiones condicionales, esta instrucción IF debe asociarse a una coincidencia. Si no se han definido ningún expresiones condicionales adicionales, esta coincidencia determina criterio Hola que debe cumplirse antes de que un conjunto de características puede ser solicitud tooa aplicada.
AND IF | Una expresión si y solo puede agregarse después de hello siguientes tipos de expresiones condicional: IF, y si. Indica que hay otra condición que debe cumplirse para instrucción IF inicial de Hola.
ELSE IF| Una expresión o si especifica una condición alternativa que debe cumplirse antes de que realiza un conjunto de características específicas toothis instrucción ELSE IF. presencia de Hola de una instrucción ELSE IF indica final hello de la instrucción anterior Hola. expresión condicional solo Hola que se puede colocar después de una instrucción ELSE IF es otra instrucción ELSE IF. Esto significa que una instrucción IF ELSE solo puede ser toospecify usa una única condición adicional que tiene toobe cumplen.

**Ejemplo**: ![Condición de coincidencia de red CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Una regla subsiguientes puede invalidar las acciones de hello especificadas por una regla anterior. Ejemplo: Una regla de detección de todo protege todas las solicitudes a través de la autenticación basada en token. Se puede crear otra regla justo debajo de ella toomake una excepción para ciertos tipos de solicitudes.

### <a name="next-steps"></a>Pasos siguientes
* [Información general de la red CDN de Azure](cdn-overview.md)
* [Referencia del motor de reglas](cdn-rules-engine-reference.md)
* [Condiciones de coincidencia del motor de reglas](cdn-rules-engine-reference-match-conditions.md)
* [Funciones del motor de reglas](cdn-rules-engine-reference-features.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
