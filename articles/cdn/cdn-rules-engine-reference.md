---
title: referencia de motor de reglas de aaaAzure CDN | Documentos de Microsoft
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Motor de reglas de la red CDN de Azure
Este tema enumeran descripciones detalladas de las condiciones de coincidencia disponible de Hola y características del red de entrega de contenido (CDN) para Azure [motor de reglas de](cdn-rules-engine.md).

Hola motor de reglas de HTTP está diseñado toobe Hola determinan de forma definitiva en tipos específicos de las solicitudes se procesan mediante CDN Hola.

**Usos habituales**:

- Invalidar o definir una directiva de memoria caché personalizada.
- Proteger o denegar las solicitudes de contenido confidencial.
- Redirigir solicitudes.
- Almacenar datos de registro personalizados.

## <a name="terminology"></a>Terminología
Una regla está definida mediante el uso de Hola de [ **expresiones condicionales**](cdn-rules-engine-reference-conditional-expressions.md), [ **coincide con**](cdn-rules-engine-reference-match-conditions.md), y [  **características**](cdn-rules-engine-reference-features.md). Estos elementos se resaltan en hello siguiente ilustración.

 ![Condición de coincidencia de red CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Sintaxis

manera de Hello en el que se tratarán los caracteres especiales varía correspondiente toohow una condición de coincidencia o valores de texto de identificadores de características. Una condición de coincidencia o característica puede interpretar el texto en uno de hello siguientes maneras:

1. [**Valores literales**](#literal-values) 
2. [**Valores de carácter comodín**](#wildcard-values)
3. [**Expresiones regulares**](#regular-expressions)

### <a name="literal-values"></a>Valores literales
Texto que se interpreta como un valor literal tratará todos los caracteres especiales, con excepción de Hola de símbolos de % de hello, como parte del valor de Hola que debe coincidir. En otras palabras, un literal coincide con la condición establecida demasiado`\'*'\` sólo se pueden lograr al que valor exacto (es decir, `\'*'\`) se encuentra.
 
Un símbolo de porcentaje es dirección URL de tooindicate usa codificación (p. ej., `%20`).

### <a name="wildcard-values"></a>Valores de carácter comodín
Texto que se interpreta como un valor comodín que asignará caracteres de toospecial un significado adicional. Hello en la tabla siguiente describe cómo se interpretarán Hola siguiendo el juego de caracteres.

Character | Descripción
----------|------------
\ | Una barra diagonal inversa es tooescape usa ninguno de los caracteres de hello especificada en esta tabla. Una barra diagonal inversa debe especificarse directamente antes de carácter especial de Hola que debe ser caracteres de escape.<br/>Por ejemplo, según la sintaxis de hello convierte un asterisco:`\*`
% | Un símbolo de porcentaje es dirección URL de tooindicate usa codificación (p. ej., `%20`).
* | Un asterisco es un carácter comodín que representa uno o más caracteres.
Espacio | Un carácter de espacio indica que se puede satisfacer una condición de coincidencia, ya sea de hello especificado valores o patrones.
'valor' | Las comillas simples no tienen un significado especial. Sin embargo, se utiliza un conjunto de comillas simples tooindicate que debe ser un valor que se trata como un valor literal. Se puede utilizar en hello siguientes maneras:<br><br/>-Permite un toobe de condición de coincidencia que se cumple cuando Hola especifica el valor coincide con cualquier parte del valor de comparación de Hola.  Por ejemplo, `'ma'` coincidiría con cualquiera de hello siguientes cadenas: <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-Permite un toobe de carácter especial especificado como un carácter literal. Por ejemplo, puede especificar un carácter de espacio literal incluyendo un carácter de espacio en un conjunto de comillas simples (es decir, `' '` o `'sample value'`).<br/>-Permite un toobe de valor en blanco especificado. Especifique un valor en blanco mediante la especificación de un conjunto de comillas simples (es decir, '').<br /><br/>**Importante:**<br/>-Si Hola especifica el valor no contiene un carácter comodín, a continuación, lo automáticamente se considerarán un valor literal. Esto significa que no es necesario toospecify un conjunto de comillas simples.<br/>- Si una barra diagonal inversa no aplica el escape a otro carácter de esta tabla, se omitirá cuando se especifique dentro de un conjunto de comillas simples.<br/>-Otra manera toospecify un carácter especial como un carácter literal es tooescape mediante una barra diagonal inversa (es decir, `\`).

### <a name="regular-expressions"></a>Expresiones regulares

Las expresiones regulares definen un patrón que se buscará dentro de un valor de texto. Notación de expresiones regulares define variedad de tooa significados concretos de símbolos. Hello tabla siguiente indica cómo especiales caracteres se tratan las condiciones de coincidencia y características que admiten expresiones regulares.

Carácter especial | Descripción
------------------|------------
\ | Una barra diagonal inversa escapes Hola carácter Hola lo sigue. Esto hace que ese toobe caracteres que se trata como un valor literal en lugar de realizar en su significado de la expresión regular. Por ejemplo, según la sintaxis de hello convierte un asterisco:`\*`
% | significado de Hola de un símbolo de porcentaje depende de su uso.<br/><br/> `%{HTTPVariable}`: esta sintaxis identifica una variable HTTP.<br/>`%{HTTPVariable%Pattern}`: Esta sintaxis utiliza un tooidentify de símbolo de porcentaje HTTP variable y como un delimitador.<br />`\%`: Un símbolo de porcentaje de secuencias de escape permite toobe utilizado como un valor literal o una codificación de dirección URL de tooindicate (p. ej., `\%20`).
* | Un asterisco permite Hola anterior toobe de caracteres que coincide con cero o más veces. 
Espacio | Normalmente, un carácter de espacio se trata como un carácter literal. 
'valor' | Las comillas simples se tratan como caracteres literales. Un conjunto de comillas simples no tiene un significado especial.


## <a name="next-steps"></a>Pasos siguientes
* [Condiciones de coincidencia del motor de reglas](cdn-rules-engine-reference-match-conditions.md)
* [Expresiones condicionales del motor de reglas](cdn-rules-engine-reference-conditional-expressions.md)
* [Funciones del motor de reglas](cdn-rules-engine-reference-features.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
* [Información general de la red CDN de Azure](cdn-overview.md)
