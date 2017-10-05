---
title: Referencia de la sintaxis de SQLRuleAction en Azure | Microsoft Docs
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
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="05be2-103">Sintaxis de SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="05be2-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="05be2-104">*SqlRuleAction* es una instancia de la clase [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) y representa un conjunto de acciones escritos en una sintaxis basada en el lenguaje SQL que se realizan en un objeto [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="05be2-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="05be2-105">Este tema describe los detalles de la gramática de acción de reglas SQL.</span><span class="sxs-lookup"><span data-stu-id="05be2-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="05be2-106">Argumentos</span><span class="sxs-lookup"><span data-stu-id="05be2-106">Arguments</span></span>  
  
-   <span data-ttu-id="05be2-107">`<scope>` es una cadena opcional que indica el ámbito de `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="05be2-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="05be2-108">Los valores válidos son `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="05be2-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="05be2-109">El valor `sys` indica el ámbito del sistema, donde `<property_name>` es un nombre de propiedad pública de [Clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="05be2-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="05be2-110">`user` indica el ámbito de usuario, donde `<property_name>` es una clave del diccionario [Clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="05be2-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="05be2-111">El ámbito de `user` es el predeterminado si no se especifica `<scope>`.</span><span class="sxs-lookup"><span data-stu-id="05be2-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="05be2-112">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-112">Remarks</span></span>  

<span data-ttu-id="05be2-113">Un intento de acceso a una propiedad de sistema que no existe es un error, mientras que uno a una propiedad de usuario inexistente, no lo es.</span><span class="sxs-lookup"><span data-stu-id="05be2-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="05be2-114">En su lugar, una propiedad de usuario inexistente internamente se evalúa como un valor desconocido.</span><span class="sxs-lookup"><span data-stu-id="05be2-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="05be2-115">Un valor desconocido se trata de una forma especial durante la evaluación de operador.</span><span class="sxs-lookup"><span data-stu-id="05be2-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="05be2-116">property_name</span><span class="sxs-lookup"><span data-stu-id="05be2-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="05be2-117">Argumentos</span><span class="sxs-lookup"><span data-stu-id="05be2-117">Arguments</span></span>  
 <span data-ttu-id="05be2-118">`<regular_identifier>` es una cadena que se representa mediante la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="05be2-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="05be2-119">Es decir, cualquier cadena que empieza por una letra y va seguida de uno o varios dígitos, letras o guiones bajo.</span><span class="sxs-lookup"><span data-stu-id="05be2-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="05be2-120">`[:IsLetter:]` significa cualquier carácter Unicode que se clasifica como una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="05be2-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="05be2-121">`System.Char.IsLetter(c)` devuelve `true` si `c` es una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="05be2-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="05be2-122">`[:IsDigit:]` significa cualquier carácter Unicode que se clasifica como un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="05be2-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="05be2-123">`System.Char.IsDigit(c)` devuelve `true` si `c` es un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="05be2-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="05be2-124">`<regular_identifier>` no puede ser una palabra clave reservada.</span><span class="sxs-lookup"><span data-stu-id="05be2-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="05be2-125">`<delimited_identifier>` es cualquier cadena que se incluye con corchetes izquierdos y derechos ([]).</span><span class="sxs-lookup"><span data-stu-id="05be2-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="05be2-126">Un corchete derecho se representan como dos corchetes derechos.</span><span class="sxs-lookup"><span data-stu-id="05be2-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="05be2-127">A continuación, se muestran ejemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="05be2-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="05be2-128">`<quoted_identifier>` es cualquier cadena que se incluye entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="05be2-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="05be2-129">Las comillas dobles en el identificador se representan como dos comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="05be2-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="05be2-130">No se recomienda utilizar identificadores entre comillas, ya que pueden confundirse fácilmente con una constante de cadena.</span><span class="sxs-lookup"><span data-stu-id="05be2-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="05be2-131">Si es posible, utilice un identificador delimitado.</span><span class="sxs-lookup"><span data-stu-id="05be2-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="05be2-132">A continuación, se muestra un ejemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="05be2-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="05be2-133">Patrón</span><span class="sxs-lookup"><span data-stu-id="05be2-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="05be2-134">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-134">Remarks</span></span>
  
 <span data-ttu-id="05be2-135">`<pattern>` debe ser una expresión que se evalúa como una cadena.</span><span class="sxs-lookup"><span data-stu-id="05be2-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="05be2-136">Se utiliza como patrón para el operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="05be2-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="05be2-137">Puede contener los siguientes caracteres comodín:</span><span class="sxs-lookup"><span data-stu-id="05be2-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="05be2-138">`%`: cualquier cadena de cero o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="05be2-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="05be2-139">`_`: cualquier carácter individual.</span><span class="sxs-lookup"><span data-stu-id="05be2-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="05be2-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="05be2-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="05be2-141">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-141">Remarks</span></span>
  
 <span data-ttu-id="05be2-142">`<escape_char>` debe ser una expresión que se evalúa como una cadena de longitud 1.</span><span class="sxs-lookup"><span data-stu-id="05be2-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="05be2-143">Se utiliza como carácter de escape para el operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="05be2-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="05be2-144">Por ejemplo, `property LIKE 'ABC\%' ESCAPE '\'` coincide con `ABC%`, en lugar de con una cadena que comienza con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="05be2-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="05be2-145">constant</span><span class="sxs-lookup"><span data-stu-id="05be2-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="05be2-146">Argumentos</span><span class="sxs-lookup"><span data-stu-id="05be2-146">Arguments</span></span>  
  
-   <span data-ttu-id="05be2-147">`<integer_constant>` es una cadena de números que no se incluyen entre comillas y no contienen decimales.</span><span class="sxs-lookup"><span data-stu-id="05be2-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="05be2-148">Los valores se almacenan como `System.Int64` internamente y siguen el mismo intervalo.</span><span class="sxs-lookup"><span data-stu-id="05be2-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="05be2-149">A continuación, se muestran ejemplos de constantes largas:</span><span class="sxs-lookup"><span data-stu-id="05be2-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="05be2-150">`<decimal_constant>` es una cadena de números que no se incluyen entre comillas y contienen un separador decimal.</span><span class="sxs-lookup"><span data-stu-id="05be2-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="05be2-151">Los valores se almacenan como `System.Double` internamente y siguen el mismo intervalo o la misma precisión.</span><span class="sxs-lookup"><span data-stu-id="05be2-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="05be2-152">En una versión futura, este número podría almacenarse en un tipo de datos diferente para admitir la semántica de número exacto. Por lo tanto, no debe confiar en el hecho de que el tipo de datos subyacente es `System.Double` en `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="05be2-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="05be2-153">A continuación, se muestran ejemplos de constantes decimales:</span><span class="sxs-lookup"><span data-stu-id="05be2-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="05be2-154">`<approximate_number_constant>` es un número escrito en la notación científica.</span><span class="sxs-lookup"><span data-stu-id="05be2-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="05be2-155">Los valores se almacenan como `System.Double` internamente y siguen el mismo intervalo o la misma precisión.</span><span class="sxs-lookup"><span data-stu-id="05be2-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="05be2-156">A continuación, se muestran ejemplos de constantes de número aproximado:</span><span class="sxs-lookup"><span data-stu-id="05be2-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="05be2-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="05be2-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="05be2-158">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-158">Remarks</span></span>
  
<span data-ttu-id="05be2-159">Las constantes booleanas se representan mediante las palabras clave `TRUE` o `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="05be2-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="05be2-160">Los valores se almacenan como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="05be2-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="05be2-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="05be2-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="05be2-162">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-162">Remarks</span></span>
  
<span data-ttu-id="05be2-163">Las constantes de cadena se incluyen entre comillas simples y contienen caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="05be2-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="05be2-164">Una comilla simple incrustada en una constante de cadena se representan como dos comillas simples.</span><span class="sxs-lookup"><span data-stu-id="05be2-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="05be2-165">function</span><span class="sxs-lookup"><span data-stu-id="05be2-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="05be2-166">Comentarios</span><span class="sxs-lookup"><span data-stu-id="05be2-166">Remarks</span></span>  

<span data-ttu-id="05be2-167">La función `newid()` devuelve un elemento **System.Guid** generado por el método `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="05be2-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="05be2-168">La función `property(name)` devuelve el valor de la propiedad a la que hace referencia `name`.</span><span class="sxs-lookup"><span data-stu-id="05be2-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="05be2-169">El valor `name` puede ser cualquier expresión válida que devuelve un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="05be2-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="05be2-170">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="05be2-170">Considerations</span></span>

- <span data-ttu-id="05be2-171">SET se usa para crear una nueva propiedad o actualizar el valor de una propiedad existente.</span><span class="sxs-lookup"><span data-stu-id="05be2-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="05be2-172">REMOVE se utiliza para quitar una propiedad.</span><span class="sxs-lookup"><span data-stu-id="05be2-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="05be2-173">SET realiza la conversión implícita si es posible cuando el tipo de expresión y el tipo de propiedad existentes son diferentes.</span><span class="sxs-lookup"><span data-stu-id="05be2-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="05be2-174">La acción no se realiza correctamente si se hace referencia a propiedades del sistema inexistentes.</span><span class="sxs-lookup"><span data-stu-id="05be2-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="05be2-175">La acción no se realiza correctamente si se hace referencia a propiedades del usuario inexistentes.</span><span class="sxs-lookup"><span data-stu-id="05be2-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="05be2-176">Una propiedad de usuario inexistente se evalúa como desconocida internamente siguiendo la misma semántica que [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) al evaluar los operadores.</span><span class="sxs-lookup"><span data-stu-id="05be2-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05be2-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05be2-177">Next steps</span></span>

- [<span data-ttu-id="05be2-178">Clase SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="05be2-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="05be2-179">Clase SQLFilter</span><span class="sxs-lookup"><span data-stu-id="05be2-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
