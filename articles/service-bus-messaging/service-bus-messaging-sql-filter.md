---
title: Referencia de la sintaxis de SQLFilter de Azure Service Bus | Microsoft Docs
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="39d48-103">Sintaxis de SQLFilter</span><span class="sxs-lookup"><span data-stu-id="39d48-103">SQLFilter syntax</span></span>

<span data-ttu-id="39d48-104">*SqlFilter* es una instancia de la [clase SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) y representa una expresión de filtro en basada en lenguaje SQL que se evalúa con respecto a un objeto [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="39d48-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="39d48-105">SqlFilter admite un subconjunto del estándar SQL-92.</span><span class="sxs-lookup"><span data-stu-id="39d48-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="39d48-106">En este tema se ofrece información sobre la gramática de SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="39d48-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="39d48-107">Argumentos</span><span class="sxs-lookup"><span data-stu-id="39d48-107">Arguments</span></span>  
  
-   <span data-ttu-id="39d48-108">`<scope>` es una cadena opcional que indica el ámbito de `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="39d48-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="39d48-109">Los valores válidos son `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="39d48-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="39d48-110">El valor `sys` indica el ámbito del sistema, donde `<property_name>` es un nombre de propiedad pública de la [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="39d48-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="39d48-111">`user` indica el ámbito de usuario, donde `<property_name>` es una clave del diccionario de la [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="39d48-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="39d48-112">El ámbito de `user` es el predeterminado si no se especifica `<scope>`.</span><span class="sxs-lookup"><span data-stu-id="39d48-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="39d48-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-113">Remarks</span></span>

<span data-ttu-id="39d48-114">Un intento de acceso a una propiedad de sistema que no existe es un error, mientras que uno a una propiedad de usuario inexistente, no lo es.</span><span class="sxs-lookup"><span data-stu-id="39d48-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="39d48-115">En su lugar, una propiedad de usuario inexistente internamente se evalúa como un valor desconocido.</span><span class="sxs-lookup"><span data-stu-id="39d48-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="39d48-116">Un valor desconocido se trata de una forma especial durante la evaluación de operador.</span><span class="sxs-lookup"><span data-stu-id="39d48-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="39d48-117">property_name</span><span class="sxs-lookup"><span data-stu-id="39d48-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="39d48-118">Argumentos</span><span class="sxs-lookup"><span data-stu-id="39d48-118">Arguments</span></span>  

 <span data-ttu-id="39d48-119">`<regular_identifier>` es una cadena que se representa mediante la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="39d48-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="39d48-120">Esta gramática significa cualquier cadena que empiece por una letra y vaya seguida de uno o varios dígitos, letras o guiones bajo.</span><span class="sxs-lookup"><span data-stu-id="39d48-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="39d48-121">`[:IsLetter:]` significa cualquier carácter Unicode que se clasifica como una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="39d48-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="39d48-122">`System.Char.IsLetter(c)` devuelve `true` si `c` es una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="39d48-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="39d48-123">`[:IsDigit:]` significa cualquier carácter Unicode que se clasifica como un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="39d48-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="39d48-124">`System.Char.IsDigit(c)` devuelve `true` si `c` es un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="39d48-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="39d48-125">`<regular_identifier>` no puede ser una palabra clave reservada.</span><span class="sxs-lookup"><span data-stu-id="39d48-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="39d48-126">`<delimited_identifier>` es cualquier cadena que se incluye con corchetes izquierdos y derechos ([]).</span><span class="sxs-lookup"><span data-stu-id="39d48-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="39d48-127">Un corchete derecho se representan como dos corchetes derechos.</span><span class="sxs-lookup"><span data-stu-id="39d48-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="39d48-128">A continuación, se muestran ejemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="39d48-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="39d48-129">`<quoted_identifier>` es cualquier cadena que se incluye entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="39d48-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="39d48-130">Las comillas dobles en el identificador se representan como dos comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="39d48-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="39d48-131">No se recomienda utilizar identificadores entre comillas, ya que pueden confundirse fácilmente con una constante de cadena.</span><span class="sxs-lookup"><span data-stu-id="39d48-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="39d48-132">Si es posible, utilice un identificador delimitado.</span><span class="sxs-lookup"><span data-stu-id="39d48-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="39d48-133">A continuación, se muestra un ejemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="39d48-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="39d48-134">Patrón</span><span class="sxs-lookup"><span data-stu-id="39d48-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="39d48-135">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-135">Remarks</span></span>
  
<span data-ttu-id="39d48-136">`<pattern>` debe ser una expresión que se evalúa como una cadena.</span><span class="sxs-lookup"><span data-stu-id="39d48-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="39d48-137">Se utiliza como patrón para el operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="39d48-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="39d48-138">Puede contener los siguientes caracteres comodín:</span><span class="sxs-lookup"><span data-stu-id="39d48-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="39d48-139">`%`: cualquier cadena de cero o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="39d48-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="39d48-140">`_`: cualquier carácter individual.</span><span class="sxs-lookup"><span data-stu-id="39d48-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="39d48-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="39d48-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="39d48-142">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-142">Remarks</span></span>  

<span data-ttu-id="39d48-143">`<escape_char>` debe ser una expresión que se evalúa como una cadena de longitud 1.</span><span class="sxs-lookup"><span data-stu-id="39d48-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="39d48-144">Se utiliza como carácter de escape para el operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="39d48-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="39d48-145">Por ejemplo, `property LIKE 'ABC\%' ESCAPE '\'` coincide con `ABC%`, en lugar de con una cadena que comienza con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="39d48-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="39d48-146">constant</span><span class="sxs-lookup"><span data-stu-id="39d48-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="39d48-147">Argumentos</span><span class="sxs-lookup"><span data-stu-id="39d48-147">Arguments</span></span>  
  
-   <span data-ttu-id="39d48-148">`<integer_constant>` es una cadena de números que no se incluyen entre comillas y no contienen decimales.</span><span class="sxs-lookup"><span data-stu-id="39d48-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="39d48-149">Los valores se almacenan como `System.Int64` internamente y siguen el mismo intervalo.</span><span class="sxs-lookup"><span data-stu-id="39d48-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="39d48-150">A continuación, se muestran ejemplos de constantes largas:</span><span class="sxs-lookup"><span data-stu-id="39d48-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="39d48-151">`<decimal_constant>` es una cadena de números que no se incluyen entre comillas y contienen un separador decimal.</span><span class="sxs-lookup"><span data-stu-id="39d48-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="39d48-152">Los valores se almacenan como `System.Double` internamente y siguen el mismo intervalo o la misma precisión.</span><span class="sxs-lookup"><span data-stu-id="39d48-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="39d48-153">En una versión futura, este número podría almacenarse en un tipo de datos diferente para admitir la semántica de número exacto. Por lo tanto, no debe confiar en el hecho de que el tipo de datos subyacente es `System.Double` en `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="39d48-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="39d48-154">A continuación, se muestran ejemplos de constantes decimales:</span><span class="sxs-lookup"><span data-stu-id="39d48-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="39d48-155">`<approximate_number_constant>` es un número escrito en la notación científica.</span><span class="sxs-lookup"><span data-stu-id="39d48-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="39d48-156">Los valores se almacenan como `System.Double` internamente y siguen el mismo intervalo o la misma precisión.</span><span class="sxs-lookup"><span data-stu-id="39d48-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="39d48-157">A continuación, se muestran ejemplos de constantes de número aproximado:</span><span class="sxs-lookup"><span data-stu-id="39d48-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="39d48-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="39d48-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="39d48-159">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-159">Remarks</span></span>  

<span data-ttu-id="39d48-160">Las constantes booleanas se representan mediante las palabras clave **TRUE** o **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="39d48-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="39d48-161">Los valores se almacenan como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="39d48-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="39d48-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="39d48-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="39d48-163">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-163">Remarks</span></span>  

<span data-ttu-id="39d48-164">Las constantes de cadena se incluyen entre comillas simples y contienen caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="39d48-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="39d48-165">Una comilla simple incrustada en una constante de cadena se representan como dos comillas simples.</span><span class="sxs-lookup"><span data-stu-id="39d48-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="39d48-166">function</span><span class="sxs-lookup"><span data-stu-id="39d48-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="39d48-167">Comentarios</span><span class="sxs-lookup"><span data-stu-id="39d48-167">Remarks</span></span>
  
<span data-ttu-id="39d48-168">La función `newid()` devuelve un elemento **System.Guid** generado por el método `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="39d48-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="39d48-169">La función `property(name)` devuelve el valor de la propiedad a la que hace referencia `name`.</span><span class="sxs-lookup"><span data-stu-id="39d48-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="39d48-170">El valor `name` puede ser cualquier expresión válida que devuelve un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="39d48-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="39d48-171">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="39d48-171">Considerations</span></span>
  
<span data-ttu-id="39d48-172">Tenga en cuenta la siguiente semántica de [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter):</span><span class="sxs-lookup"><span data-stu-id="39d48-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="39d48-173">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="39d48-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="39d48-174">Los operadores siguen la semántica de conversión implícita de C# siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="39d48-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="39d48-175">Las propiedades del sistema son propiedades públicas expuestas en instancias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="39d48-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="39d48-176">Tenga en cuenta la siguiente semántica de `IS [NOT] NULL`:</span><span class="sxs-lookup"><span data-stu-id="39d48-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="39d48-177">`property IS NULL` se evalúa como `true` si no existe la propiedad o valor de la propiedad es `null`.</span><span class="sxs-lookup"><span data-stu-id="39d48-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="39d48-178">Semántica de evaluación de propiedades</span><span class="sxs-lookup"><span data-stu-id="39d48-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="39d48-179">Un intento de evaluar una propiedad no existente del sistema genera una excepción [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception).</span><span class="sxs-lookup"><span data-stu-id="39d48-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="39d48-180">Una propiedad que no existe se evalúa internamente como **valor desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="39d48-181">Evaluación desconocida en operadores aritméticos:</span><span class="sxs-lookup"><span data-stu-id="39d48-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="39d48-182">Para los operadores binarios, si la parte izquierda o derecha de los operandos se evalúa como **valor desconocido**, el resultado será **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="39d48-183">Para los operadores unarios, si un operando se evalúa como **desconocido**, el resultado será **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="39d48-184">Evaluación desconocida en los operadores de comparación binaria:</span><span class="sxs-lookup"><span data-stu-id="39d48-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="39d48-185">Si la parte izquierda o derecha de los operandos se evalúa como **valor desconocido**, el resultado será **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="39d48-186">Evaluación desconocida en `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="39d48-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="39d48-187">Si cualquier operando se evalúa como **desconocido**, el resultado es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="39d48-188">Evaluación desconocida en `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="39d48-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="39d48-189">Si el operando izquierdo se evalúa como **desconocido**, el resultado es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="39d48-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="39d48-190">Evaluación desconocida en el operador **AND**:</span><span class="sxs-lookup"><span data-stu-id="39d48-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="39d48-191">Evaluación desconocida en el operador **OR**:</span><span class="sxs-lookup"><span data-stu-id="39d48-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="39d48-192">Semántica de enlace de operadores</span><span class="sxs-lookup"><span data-stu-id="39d48-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="39d48-193">Los operadores de comparación, como `>`, `>=`, `<`, `<=`, `!=` y `=`, siguen la misma semántica que el enlace de operadores de C# en promociones de tipo de datos y conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="39d48-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="39d48-194">Los operadores aritméticos, como `+`, `-`, `*`, `/` y `%`, siguen la misma semántica que el enlace de operadores de C# en promociones de tipo de datos y conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="39d48-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39d48-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39d48-195">Next steps</span></span>

- [<span data-ttu-id="39d48-196">Clase SQLFilter</span><span class="sxs-lookup"><span data-stu-id="39d48-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="39d48-197">Clase SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="39d48-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)