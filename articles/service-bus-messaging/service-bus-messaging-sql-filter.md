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
# <a name="sqlfilter-syntax"></a><span data-ttu-id="d0bdf-103">Sintaxis de SQLFilter</span><span class="sxs-lookup"><span data-stu-id="d0bdf-103">SQLFilter syntax</span></span>

<span data-ttu-id="d0bdf-104">A *SqlFilter* es una instancia de hello [SqlFilter clase](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)y representa una expresión de filtro basada en lenguaje SQL que se evalúa con un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="d0bdf-105">Un SqlFilter admite un subconjunto del estándar SQL-92 Hola.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="d0bdf-106">En este tema se ofrece información sobre la gramática de SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="d0bdf-107">Argumentos</span><span class="sxs-lookup"><span data-stu-id="d0bdf-107">Arguments</span></span>  
  
-   <span data-ttu-id="d0bdf-108">`<scope>`es una cadena opcional que indica el ámbito de Hola de hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="d0bdf-109">Los valores válidos son `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="d0bdf-110">Hola `sys` valor indica el ámbito del sistema donde `<property_name>` es un nombre de propiedad pública de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="d0bdf-111">`user`indica el ámbito de usuario donde `<property_name>` es una clave de hello [clase BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) diccionario.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="d0bdf-112">`user`ámbito es el ámbito predeterminado de hello si `<scope>` no se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d0bdf-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-113">Remarks</span></span>

<span data-ttu-id="d0bdf-114">Un intento de tooaccess una propiedad inexistente por el sistema es un error, mientras que una propiedad de usuario de tooaccess un inexistente intento no es un error.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="d0bdf-115">En su lugar, una propiedad de usuario inexistente internamente se evalúa como un valor desconocido.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="d0bdf-116">Un valor desconocido se trata de una forma especial durante la evaluación de operador.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="d0bdf-117">property_name</span><span class="sxs-lookup"><span data-stu-id="d0bdf-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="d0bdf-118">Argumentos</span><span class="sxs-lookup"><span data-stu-id="d0bdf-118">Arguments</span></span>  

 <span data-ttu-id="d0bdf-119">`<regular_identifier>`es una cadena representada por hello después de expresión regular:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="d0bdf-120">Esta gramática significa cualquier cadena que empiece por una letra y vaya seguida de uno o varios dígitos, letras o guiones bajo.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="d0bdf-121">`[:IsLetter:]` significa cualquier carácter Unicode que se clasifica como una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="d0bdf-122">`System.Char.IsLetter(c)` devuelve `true` si `c` es una letra Unicode.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="d0bdf-123">`[:IsDigit:]` significa cualquier carácter Unicode que se clasifica como un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="d0bdf-124">`System.Char.IsDigit(c)` devuelve `true` si `c` es un dígito Unicode.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="d0bdf-125">`<regular_identifier>` no puede ser una palabra clave reservada.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="d0bdf-126">`<delimited_identifier>` es cualquier cadena que se incluye con corchetes izquierdos y derechos ([]).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="d0bdf-127">Un corchete derecho se representan como dos corchetes derechos.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="d0bdf-128">Hello siguientes son ejemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="d0bdf-129">`<quoted_identifier>` es cualquier cadena que se incluye entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="d0bdf-130">Las comillas dobles en el identificador se representan como dos comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="d0bdf-131">No se recomienda toouse identificadores entrecomillados, ya que pueden confundirse fácilmente con una constante de cadena.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="d0bdf-132">Si es posible, utilice un identificador delimitado.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="d0bdf-133">Hello aquí te mostramos un ejemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="d0bdf-134">Patrón</span><span class="sxs-lookup"><span data-stu-id="d0bdf-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="d0bdf-135">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-135">Remarks</span></span>
  
<span data-ttu-id="d0bdf-136">`<pattern>` debe ser una expresión que se evalúa como una cadena.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="d0bdf-137">Se utiliza como patrón para hello LIKE (operador).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="d0bdf-138">Puede contener Hola siguientes caracteres comodín:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="d0bdf-139">`%`: cualquier cadena de cero o más caracteres.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="d0bdf-140">`_`: cualquier carácter individual.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="d0bdf-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="d0bdf-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="d0bdf-142">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-142">Remarks</span></span>  

<span data-ttu-id="d0bdf-143">`<escape_char>` debe ser una expresión que se evalúa como una cadena de longitud 1.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="d0bdf-144">Se utiliza como carácter de escape para hello LIKE (operador).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="d0bdf-145">Por ejemplo, `property LIKE 'ABC\%' ESCAPE '\'` coincide con `ABC%`, en lugar de con una cadena que comienza con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="d0bdf-146">constant</span><span class="sxs-lookup"><span data-stu-id="d0bdf-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="d0bdf-147">Argumentos</span><span class="sxs-lookup"><span data-stu-id="d0bdf-147">Arguments</span></span>  
  
-   <span data-ttu-id="d0bdf-148">`<integer_constant>` es una cadena de números que no se incluyen entre comillas y no contienen decimales.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="d0bdf-149">Hola valores se almacenan como `System.Int64` internamente, y seguimiento Hola mismo intervalo.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="d0bdf-150">A continuación, se muestran ejemplos de constantes largas:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="d0bdf-151">`<decimal_constant>` es una cadena de números que no se incluyen entre comillas y contienen un separador decimal.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="d0bdf-152">Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="d0bdf-153">En una versión futura, este número puede almacenarse en una datos diferentes toosupport exacta numérica la semántica de tipos, por lo que no deben depender Hola hechos Hola subyacente es el tipo de datos `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="d0bdf-154">siguiente Hola es ejemplos de constantes de tipo decimal:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="d0bdf-155">`<approximate_number_constant>` es un número escrito en la notación científica.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="d0bdf-156">Hola valores se almacenan como `System.Double` internamente y seguir Hola mismo intervalo y precisión.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="d0bdf-157">siguiente Hola es ejemplos de constantes de número aproximados:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="d0bdf-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="d0bdf-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="d0bdf-159">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-159">Remarks</span></span>  

<span data-ttu-id="d0bdf-160">Constantes booleanas se representan mediante palabras clave de hello **TRUE** o **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="d0bdf-161">Hola valores se almacenan como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="d0bdf-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="d0bdf-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="d0bdf-163">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-163">Remarks</span></span>  

<span data-ttu-id="d0bdf-164">Las constantes de cadena se incluyen entre comillas simples y contienen caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="d0bdf-165">Una comilla simple incrustada en una constante de cadena se representan como dos comillas simples.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="d0bdf-166">function</span><span class="sxs-lookup"><span data-stu-id="d0bdf-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="d0bdf-167">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bdf-167">Remarks</span></span>
  
<span data-ttu-id="d0bdf-168">Hola `newid()` función devuelve un **System.Guid** generados por hello `System.Guid.NewGuid()` método.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="d0bdf-169">Hola `property(name)` función devuelve el valor de Hola de propiedad Hola al que hace referencia `name`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="d0bdf-170">Hola `name` valor puede ser cualquier expresión válida que devuelve un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="d0bdf-171">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="d0bdf-171">Considerations</span></span>
  
<span data-ttu-id="d0bdf-172">Tenga en cuenta los siguiente hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semántica:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="d0bdf-173">Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="d0bdf-174">Los operadores siguen la semántica de conversión implícita de C# siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="d0bdf-175">Las propiedades del sistema son propiedades públicas expuestas en instancias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="d0bdf-176">Tenga en cuenta los siguiente hello `IS [NOT] NULL` semántica:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="d0bdf-177">`property IS NULL`se evalúa como `true` si cualquiera de estas propiedades de hello no existe u Hola el valor de la propiedad es `null`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="d0bdf-178">Semántica de evaluación de propiedades</span><span class="sxs-lookup"><span data-stu-id="d0bdf-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="d0bdf-179">Un tooevaluate de intento de una propiedad inexistente por el sistema produce una [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) excepción.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="d0bdf-180">Una propiedad que no existe se evalúa internamente como **valor desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="d0bdf-181">Evaluación desconocida en operadores aritméticos:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="d0bdf-182">Para los operadores binarios, si bien Hola izquierda o derecha de los operandos se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="d0bdf-183">Para los operadores unarios, si un operando se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="d0bdf-184">Evaluación desconocida en los operadores de comparación binaria:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="d0bdf-185">Si bien Hola izquierda o derecha de los operandos se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="d0bdf-186">Evaluación desconocida en `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="d0bdf-187">Si cualquier operando se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="d0bdf-188">Evaluación desconocida en `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="d0bdf-189">Si Hola operando izquierdo se evalúa como **desconocido**, entonces el resultado de hello es **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="d0bdf-190">Evaluación desconocida en el operador **AND**:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="d0bdf-191">Evaluación desconocida en el operador **OR**:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="d0bdf-192">Semántica de enlace de operadores</span><span class="sxs-lookup"><span data-stu-id="d0bdf-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="d0bdf-193">Operadores de comparación, como `>`, `>=`, `<`, `<=`, `!=`, y `=` seguimiento Hola misma semántica que el enlace de datos de operador de hello C# escriba promociones y las conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="d0bdf-194">Operadores aritméticos, como `+`, `-`, `*`, `/`, y `%` seguimiento Hola misma semántica que el enlace de datos de operador de hello C# escriba promociones y las conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0bdf-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0bdf-195">Next steps</span></span>

- [<span data-ttu-id="d0bdf-196">Clase SQLFilter</span><span class="sxs-lookup"><span data-stu-id="d0bdf-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="d0bdf-197">Clase SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="d0bdf-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)