---
title: referencia de la sintaxis de aaaSQLRuleAction en Azure | Documentos de Microsoft
description: "Obtenga más información sobre la gramática de SQLRuleAction."
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="c66c1-103">Sintaxis de SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="c66c1-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="c66c1-104">A *SqlRuleAction* es una instancia de hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) clase y representa conjunto de acciones escritos en lenguaje SQL en función de sintaxis que se realizan contra un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="c66c1-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="c66c1-105">En este tema muestra detalles acerca de hello gramática de acción de regla SQL.</span><span class="sxs-lookup"><span data-stu-id="c66c1-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="c66c1-106">Argumentos</span><span class="sxs-lookup"><span data-stu-id="c66c1-106">Arguments</span></span>  
  
-   <span data-ttu-id="c66c1-107">`<scope>`es una cadena opcional que indica el ámbito de Hola de hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="c66c1-108">Los valores válidos son `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="c66c1-109">Hola `sys` valor indica el ámbito del sistema donde `<property_name>` es un nombre de propiedad pública de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="c66c1-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="c66c1-110">`user`indica el ámbito de usuario donde `<property_name>` es una clave de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) diccionario.</span><span class="sxs-lookup"><span data-stu-id="c66c1-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="c66c1-111">`user`ámbito es el ámbito predeterminado de hello si `<scope>` no se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="c66c1-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-112">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-112">Remarks</span></span>  

<span data-ttu-id="c66c1-113">Un intento de tooaccess una propiedad inexistente por el sistema es un error, mientras que una propiedad de usuario de tooaccess un inexistente intento no es un error.</span><span class="sxs-lookup"><span data-stu-id="c66c1-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="c66c1-114">En su lugar, una propiedad de usuario inexistente internamente se evalúa como un valor desconocido.</span><span class="sxs-lookup"><span data-stu-id="c66c1-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="c66c1-115">Un valor desconocido se trata de una forma especial durante la evaluación de operador.</span><span class="sxs-lookup"><span data-stu-id="c66c1-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="c66c1-116">property_name</span><span class="sxs-lookup"><span data-stu-id="c66c1-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="c66c1-117">Argumentos</span><span class="sxs-lookup"><span data-stu-id="c66c1-117">Arguments</span></span>  
 <span data-ttu-id="c66c1-118">`<regular_identifier>`es una cadena representada por hello después de expresión regular:</span><span class="sxs-lookup"><span data-stu-id="c66c1-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="c66c1-119">Es decir, cualquier cadena que empieza por una letra y va seguida de uno o varios dígitos, letras o guiones bajo.</span><span class="sxs-lookup"><span data-stu-id="c66c1-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="c66c1-120">`[:IsLetter:]` significa cualquier carácter Unicode que se clasifica como una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="c66c1-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="c66c1-121">`System.Char.IsLetter(c)` devuelve `true` si `c` es una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="c66c1-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="c66c1-122">`[:IsDigit:]` significa cualquier carácter Unicode que se clasifica como un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="c66c1-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="c66c1-123">`System.Char.IsDigit(c)` devuelve `true` si `c` es un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="c66c1-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="c66c1-124">`<regular_identifier>` no puede ser una palabra clave reservada.</span><span class="sxs-lookup"><span data-stu-id="c66c1-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="c66c1-125">`<delimited_identifier>` es cualquier cadena que se incluye con corchetes izquierdos y derechos ([]).</span><span class="sxs-lookup"><span data-stu-id="c66c1-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="c66c1-126">Un corchete derecho se representan como dos corchetes derechos.</span><span class="sxs-lookup"><span data-stu-id="c66c1-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="c66c1-127">Hello siguientes son ejemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="c66c1-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="c66c1-128">`<quoted_identifier>` es cualquier cadena que se incluye entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="c66c1-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="c66c1-129">Las comillas dobles en el identificador se representan como dos comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="c66c1-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="c66c1-130">No se recomienda toouse identificadores entrecomillados, ya que pueden confundirse fácilmente con una constante de cadena.</span><span class="sxs-lookup"><span data-stu-id="c66c1-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="c66c1-131">Si es posible, utilice un identificador delimitado.</span><span class="sxs-lookup"><span data-stu-id="c66c1-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="c66c1-132">Hello aquí te mostramos un ejemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="c66c1-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="c66c1-133">Patrón</span><span class="sxs-lookup"><span data-stu-id="c66c1-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-134">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-134">Remarks</span></span>
  
 <span data-ttu-id="c66c1-135">`<pattern>` debe ser una expresión que se evalúa como una cadena.</span><span class="sxs-lookup"><span data-stu-id="c66c1-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="c66c1-136">Se utiliza como patrón para hello LIKE (operador).</span><span class="sxs-lookup"><span data-stu-id="c66c1-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="c66c1-137">Puede contener Hola siguientes caracteres comodín:</span><span class="sxs-lookup"><span data-stu-id="c66c1-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="c66c1-138">`%`: cualquier cadena de cero o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="c66c1-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="c66c1-139">`_`: cualquier carácter individual.</span><span class="sxs-lookup"><span data-stu-id="c66c1-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="c66c1-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="c66c1-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-141">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-141">Remarks</span></span>
  
 <span data-ttu-id="c66c1-142">`<escape_char>` debe ser una expresión que se evalúa como una cadena de longitud 1.</span><span class="sxs-lookup"><span data-stu-id="c66c1-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="c66c1-143">Se utiliza como carácter de escape para hello LIKE (operador).</span><span class="sxs-lookup"><span data-stu-id="c66c1-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="c66c1-144">Por ejemplo, `property LIKE 'ABC\%' ESCAPE '\'` coincide con `ABC%`, en lugar de con una cadena que comienza con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="c66c1-145">constant</span><span class="sxs-lookup"><span data-stu-id="c66c1-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="c66c1-146">Argumentos</span><span class="sxs-lookup"><span data-stu-id="c66c1-146">Arguments</span></span>  
  
-   <span data-ttu-id="c66c1-147">`<integer_constant>` es una cadena de números que no se incluyen entre comillas y no contienen decimales.</span><span class="sxs-lookup"><span data-stu-id="c66c1-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="c66c1-148">Hola valores se almacenan como `System.Int64` internamente, y seguimiento Hola mismo intervalo.</span><span class="sxs-lookup"><span data-stu-id="c66c1-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="c66c1-149">siguiente Hola es ejemplos de constantes largo:</span><span class="sxs-lookup"><span data-stu-id="c66c1-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="c66c1-150">`<decimal_constant>` es una cadena de números que no se incluyen entre comillas y contienen un separador decimal.</span><span class="sxs-lookup"><span data-stu-id="c66c1-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="c66c1-151">Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión.</span><span class="sxs-lookup"><span data-stu-id="c66c1-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="c66c1-152">En una versión futura, este número puede almacenarse en una datos diferentes toosupport exacta numérica la semántica de tipos, por lo que no deben depender Hola hechos Hola subyacente es el tipo de datos `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="c66c1-153">siguiente Hola es ejemplos de constantes de tipo decimal:</span><span class="sxs-lookup"><span data-stu-id="c66c1-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="c66c1-154">`<approximate_number_constant>` es un número escrito en la notación científica.</span><span class="sxs-lookup"><span data-stu-id="c66c1-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="c66c1-155">Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión.</span><span class="sxs-lookup"><span data-stu-id="c66c1-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="c66c1-156">siguiente Hola es ejemplos de constantes de número aproximados:</span><span class="sxs-lookup"><span data-stu-id="c66c1-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="c66c1-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="c66c1-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-158">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-158">Remarks</span></span>
  
<span data-ttu-id="c66c1-159">Constantes booleanas se representan mediante palabras clave de hello `TRUE` o `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="c66c1-160">Hola valores se almacenan como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="c66c1-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="c66c1-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-162">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-162">Remarks</span></span>
  
<span data-ttu-id="c66c1-163">Las constantes de cadena se incluyen entre comillas simples y contienen caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="c66c1-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="c66c1-164">Una comilla simple incrustada en una constante de cadena se representan como dos comillas simples.</span><span class="sxs-lookup"><span data-stu-id="c66c1-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="c66c1-165">function</span><span class="sxs-lookup"><span data-stu-id="c66c1-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="c66c1-166">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c66c1-166">Remarks</span></span>  

<span data-ttu-id="c66c1-167">Hola `newid()` función devuelve un **System.Guid** generados por hello `System.Guid.NewGuid()` método.</span><span class="sxs-lookup"><span data-stu-id="c66c1-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="c66c1-168">Hola `property(name)` función devuelve el valor de Hola de propiedad Hola al que hace referencia `name`.</span><span class="sxs-lookup"><span data-stu-id="c66c1-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="c66c1-169">Hola `name` valor puede ser cualquier expresión válida que devuelve un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="c66c1-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="c66c1-170">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="c66c1-170">Considerations</span></span>

- <span data-ttu-id="c66c1-171">CONJUNTO es toocreate usa un nuevo valor de Hola de propiedad o actualización de una propiedad existente.</span><span class="sxs-lookup"><span data-stu-id="c66c1-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="c66c1-172">QUITAR es tooremove usa una propiedad.</span><span class="sxs-lookup"><span data-stu-id="c66c1-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="c66c1-173">Si es posible conjunto realiza conversión implícita al tipo de expresión de Hola y el tipo de propiedad existentes de hello son diferentes.</span><span class="sxs-lookup"><span data-stu-id="c66c1-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="c66c1-174">La acción no se realiza correctamente si se hace referencia a propiedades del sistema inexistentes.</span><span class="sxs-lookup"><span data-stu-id="c66c1-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="c66c1-175">La acción no se realiza correctamente si se hace referencia a propiedades del usuario inexistentes.</span><span class="sxs-lookup"><span data-stu-id="c66c1-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="c66c1-176">Una propiedad de usuario inexistente se evalúa como "Desconocido" internamente, siguiente Hola misma semántica que [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) al evaluar los operadores.</span><span class="sxs-lookup"><span data-stu-id="c66c1-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c66c1-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c66c1-177">Next steps</span></span>

- [<span data-ttu-id="c66c1-178">Clase SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="c66c1-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="c66c1-179">Clase SQLFilter</span><span class="sxs-lookup"><span data-stu-id="c66c1-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
