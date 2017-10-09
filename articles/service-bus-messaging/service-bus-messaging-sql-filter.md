---
title: referencia de la sintaxis de SQLFilter de Bus de servicio aaaAzure | Documentos de Microsoft
description: "Obtenga más información sobre la gramática de SQLFilter."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a>Sintaxis de SQLFilter

A *SqlFilter* es una instancia de hello [SqlFilter clase](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)y representa una expresión de filtro basada en lenguaje SQL que se evalúa con un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Un SqlFilter admite un subconjunto del estándar SQL-92 Hola.  
  
 En este tema se ofrece información sobre la gramática de SqlFilter.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>Argumentos  
  
-   `<scope>`es una cadena opcional que indica el ámbito de Hola de hello `<property_name>`. Los valores válidos son `sys` o `user`. Hola `sys` valor indica el ámbito del sistema donde `<property_name>` es un nombre de propiedad pública de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`indica el ámbito de usuario donde `<property_name>` es una clave de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) diccionario. `user`ámbito es el ámbito predeterminado de hello si `<scope>` no se ha especificado.  
  
## <a name="remarks"></a>Comentarios

Un intento de tooaccess una propiedad inexistente por el sistema es un error, mientras que una propiedad de usuario de tooaccess un inexistente intento no es un error. En su lugar, una propiedad de usuario inexistente internamente se evalúa como un valor desconocido. Un valor desconocido se trata de una forma especial durante la evaluación de operador.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumentos  

 `<regular_identifier>`es una cadena representada por hello después de expresión regular:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Esta gramática significa cualquier cadena que empiece por una letra y vaya seguida de uno o varios dígitos, letras o guiones bajo.  
  
`[:IsLetter:]` significa cualquier carácter Unicode que se clasifica como una letra Unicode. `System.Char.IsLetter(c)` devuelve `true` si `c` es una letra Unicode.  
  
`[:IsDigit:]` significa cualquier carácter Unicode que se clasifica como un dígito Unicode. `System.Char.IsDigit(c)` devuelve `true` si `c` es un dígito Unicode.  
  
`<regular_identifier>` no puede ser una palabra clave reservada.  
  
`<delimited_identifier>` es cualquier cadena que se incluye con corchetes izquierdos y derechos ([]). Un corchete derecho se representan como dos corchetes derechos. Hello siguientes son ejemplos de `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` es cualquier cadena que se incluye entre comillas dobles. Las comillas dobles en el identificador se representan como dos comillas dobles. No se recomienda toouse identificadores entrecomillados, ya que pueden confundirse fácilmente con una constante de cadena. Si es posible, utilice un identificador delimitado. Hello aquí te mostramos un ejemplo de `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>Patrón  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Comentarios
  
`<pattern>` debe ser una expresión que se evalúa como una cadena. Se utiliza como patrón para hello LIKE (operador).      Puede contener Hola siguientes caracteres comodín:  
  
-   `%`: cualquier cadena de cero o más caracteres.  
  
-   `_`: cualquier carácter individual.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Comentarios  

`<escape_char>` debe ser una expresión que se evalúa como una cadena de longitud 1. Se utiliza como carácter de escape para hello LIKE (operador).  
  
 Por ejemplo, `property LIKE 'ABC\%' ESCAPE '\'` coincide con `ABC%`, en lugar de con una cadena que comienza con `ABC`.  
  
## <a name="constant"></a>constant  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumentos  
  
-   `<integer_constant>` es una cadena de números que no se incluyen entre comillas y no contienen decimales. Hola valores se almacenan como `System.Int64` internamente, y seguimiento Hola mismo intervalo.  
  
     A continuación, se muestran ejemplos de constantes largas:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` es una cadena de números que no se incluyen entre comillas y contienen un separador decimal. Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión.  
  
     En una versión futura, este número puede almacenarse en una datos diferentes toosupport exacta numérica la semántica de tipos, por lo que no deben depender Hola hechos Hola subyacente es el tipo de datos `System.Double` para `<decimal_constant>`.  
  
     siguiente Hola es ejemplos de constantes de tipo decimal:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` es un número escrito en la notación científica. Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión. siguiente Hola es ejemplos de constantes de número aproximados:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Comentarios  

Constantes booleanas se representan mediante palabras clave de hello **TRUE** o **FALSE**. Hola valores se almacenan como `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Comentarios  

Las constantes de cadena se incluyen entre comillas simples y contienen caracteres Unicode válidos. Una comilla simple incrustada en una constante de cadena se representan como dos comillas simples.  
  
## <a name="function"></a>function  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Comentarios
  
Hola `newid()` función devuelve un **System.Guid** generados por hello `System.Guid.NewGuid()` método.  
  
Hola `property(name)` función devuelve el valor de Hola de propiedad Hola al que hace referencia `name`. Hola `name` valor puede ser cualquier expresión válida que devuelve un valor de cadena.  
  
## <a name="considerations"></a>Consideraciones
  
Tenga en cuenta los siguiente hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semántica:  
  
-   Los nombres de propiedad distinguen entre mayúsculas y minúsculas.  
  
-   Los operadores siguen la semántica de conversión implícita de C# siempre que sea posible.  
  
-   Las propiedades del sistema son propiedades públicas expuestas en instancias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).  
  
    Tenga en cuenta los siguiente hello `IS [NOT] NULL` semántica:  
  
    -   `property IS NULL`se evalúa como `true` si cualquiera de estas propiedades de hello no existe u Hola el valor de la propiedad es `null`.  
  
### <a name="property-evaluation-semantics"></a>Semántica de evaluación de propiedades  
  
-   Un tooevaluate de intento de una propiedad inexistente por el sistema produce una [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) excepción.  
  
-   Una propiedad que no existe se evalúa internamente como **valor desconocido**.  
  
 Evaluación desconocida en operadores aritméticos:  
  
-   Para los operadores binarios, si bien Hola izquierda o derecha de los operandos se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.  
  
-   Para los operadores unarios, si un operando se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.  
  
 Evaluación desconocida en los operadores de comparación binaria:  
  
-   Si bien Hola izquierda o derecha de los operandos se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.  
  
 Evaluación desconocida en `[NOT] LIKE`:  
  
-   Si cualquier operando se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.  
  
 Evaluación desconocida en `[NOT] IN`:  
  
-   Si Hola operando izquierdo se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.  
  
 Evaluación desconocida en el operador **AND**:  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 Evaluación desconocida en el operador **OR**:  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>Semántica de enlace de operadores
  
-   Operadores de comparación, como `>`, `>=`, `<`, `<=`, `!=`, y `=` seguimiento Hola misma semántica que el enlace de datos de operador de hello C# escriba promociones y las conversiones implícitas.  
  
-   Operadores aritméticos, como `+`, `-`, `*`, `/`, y `%` seguimiento Hola misma semántica que el enlace de datos de operador de hello C# escriba promociones y las conversiones implícitas.

## <a name="next-steps"></a>Pasos siguientes

- [Clase SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [Clase SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)