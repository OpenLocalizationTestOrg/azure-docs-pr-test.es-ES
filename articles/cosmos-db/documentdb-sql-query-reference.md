---
título: aaa "API de documentos de base de datos de Azure Cosmos: sintaxis SQL | Descripción de Microsoft Docs": hacer referencia a documentación de hello lenguaje de consulta SQL de API de Azure Cosmos DB documentos.
servicios: cosmos db autor: mimig1 manager: editor de jhubbard: mimig documentationcenter: ''

MS.AssetId: ms.service: cosmos db ms.workload: ms.tgt_pltfrm de servicios de datos: na ms.devlang: na ms.topic: referencia ms.date: 06/13/2017 ms.author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>API de DocumentDB de Azure Cosmos DB: referencia de sintaxis SQL

Hola API de documentos de base de datos de Azure Cosmos admite consultas documentos mediante una instancia de SQL (lenguaje de consulta estructurado) familiar gramática similar en documentos JSON jerárquicos sin necesidad de esquema explícito o la creación de índices secundarios. En este tema se proporciona documentación de referencia de lenguaje de consulta SQL de la API de documentos de Hola.

Para ver un tutorial de hello lenguaje de consulta SQL de la API de documentos, consulte [consultas SQL para la API de documentos de base de datos de Azure Cosmos](documentdb-sql-query.md).  
  
También le invitamos hello toovisit [Query Playground](http://www.documentdb.com/sql/demo) donde puede probar la base de datos de Azure Cosmos y ejecutar consultas SQL contra nuestro conjunto de datos.  
  
## <a name="select-query"></a>Consulta SELECT  
Recupera documentos JSON de base de datos de Hola. Es compatible con la evaluación de expresiones, las proyecciones, el filtrado y las combinaciones.  convenciones de Hello utilizadas para describir las instrucciones SELECT de Hola se tabulan en hello sección de convenciones de sintaxis.  
  
**Sintaxis**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Comentarios**  
  
 Consulte las siguientes secciones para más información sobre las cláusulas:  
  
-   [Cláusula SELECT](#bk_select_query)  
  
-   [Cláusula FROM](#bk_from_clause)  
  
-   [Cláusula WHERE](#bk_where_clause)  
  
-   [Cláusula ORDER BY](#bk_orderby_clause)  
  
cláusulas de Hello en la instrucción SELECT de Hola se deben ordenar como se indicó anteriormente. Se puede omitir cualquiera de las cláusulas opcionales de Hola. Pero cuando se usan cláusulas opcionales, deben aparecer en el orden correcto de Hola.  
  
**Orden de procesamiento lógico de la instrucción SELECT de Hola**  
  
orden de Hello en el que se procesan las cláusulas es:  

1.  [Cláusula FROM](#bk_from_clause)  
2.  [Cláusula WHERE](#bk_where_clause)  
3.  [Cláusula ORDER BY](#bk_orderby_clause)  
4.  [Cláusula SELECT](#bk_select_query)  

Tenga en cuenta que esto es diferente del orden de hello en que aparecen en la sintaxis de Hola. Hola ordenación es tal que todos los símbolos nuevos introducidos por una cláusula procesada son visibles y pueden utilizarse en las cláusulas procesadas posteriormente. Por ejemplo, las cláusulas WHERE y SELECT pueden acceder a los alias declarados en una cláusula FROM.  

**Comentarios y caracteres de espacio en blanco**  

Todos los caracteres de espacio en blanco que no forman parte de una cadena entrecomillada o identificador entrecomillado no forman parte de la gramática del lenguaje de Hola y se omiten durante el análisis.  

lenguaje de consulta de Hello admite comentarios de estilo de T-SQL como  

-   Instrucción SQL `-- comment text [newline]`.  

Mientras que los comentarios y espacios en blanco no tiene importancia en la gramática de hello, deben ser tokens tooseparate usado. Por ejemplo: `-1e5` es un token de un solo número, mientras que `: – 1 e5` es un token de menos seguido por el número 1 y el identificador e5.  

##  <a name="bk_select_query"></a> Cláusula SELECT  
cláusulas de Hello en la instrucción SELECT de Hola se deben ordenar como se indicó anteriormente. Se puede omitir cualquiera de las cláusulas opcionales de Hola. Pero cuando se usan cláusulas opcionales, deben aparecer en el orden correcto de Hola.  

**Sintaxis**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Argumentos**  
  
 `<select_specification>`  
  
 Establece propiedades o el valor toobe seleccionado para el resultado de hello.  
  
 `'*'`  
  
Especifica que se debe recuperar el valor de hello sin realizar ningún cambio. En concreto si valor Hola procesado es un objeto, se recuperarán todas las propiedades.  
  
 `<object_property_list>`  
  
Especifica la lista de Hola de toobe de propiedades que se recuperan. Cada valor devuelto será un objeto con propiedades de hello especificadas.  
  
`VALUE`  
  
Especifica que se debe recuperar el valor JSON de hello en lugar del objeto JSON completo de Hola. Esto, a diferencia `<property_list>` no ajusta el valor de hello proyectada en un objeto.  
  
`<scalar_expression>`  
  
Calcula la expresión que representa Hola valor toobe. Consulte la sección [Expresiones escalares](#bk_scalar_expressions) para más información.  
  
**Comentarios**  
  
Hola `SELECT *` sintaxis sólo es válida si la cláusula FROM ha declarado exactamente un alias. `SELECT *` proporciona una proyección de identidad, que puede resultar útil si no se necesitan proyecciones. SELECT * solo es válida si se especifica cláusula FROM y se introdujo solo un origen de entrada.  
  
Tenga en cuenta que `SELECT <select_list>` y `SELECT *` son código sintáctico y pueden expresarse también mediante instrucciones SELECT sencillas, como se muestra a continuación.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     equivale a:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     equivale a:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Consulte también**  
  
[Expresiones escalares](#bk_scalar_expressions)  
[Cláusula SELECT](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> Cláusula FROM  
Especifica el origen de Hola o los orígenes combinados. Hola FROM cláusula es opcional. Si no se especifica, las demás cláusulas se continuarán ejecutando como si la cláusula FROM proporcionara un documento único.  
  
**Sintaxis**  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
**Argumentos**  
  
`<from_source>`  
  
Especifica un origen de datos, con o sin alias. Si no se especifica, se inferirán de hello `<collection_expression>` con las siguientes reglas:  
  
-   Si expresión de hello es un collection_name, se utilizará collection_name como alias.  
  
-   Si la expresión de hello es `<collection_expression>`, entonces se usará property_name y, a continuación, property_name como alias. Si expresión de hello es un collection_name, se utilizará collection_name como alias.  
  
AS `input_alias`.  
  
Especifica que hello `input_alias` es un conjunto de valores devueltos por hello subyacente de la expresión de colección.  
 
`input_alias` IN  
  
Especifica que hello `input_alias` debe representar el conjunto de Hola de valores obtenidos por recorrer en iteración todos los elementos de la matriz de cada matriz devuelta por hello subyacente de la expresión de colección. Se omite cualquier valor que la expresión de colección subyacente devuelva que no sea una matriz.  
  
`<collection_expression>`  
  
Especifica Hola colección expresión toobe usa documentos de hello tooretrieve.  
  
`ROOT`  
  
Especifica que debe recuperarse ese documento de Hola de forma predeterminada, colección actualmente conectada.  
  
`collection_name`  
  
Especifica que debe recuperarse ese documento de colección de hello proporcionado. Hola nombre de colección de hello debe coincidir con hello de colección de hello conectado actualmente.  
  
`input_alias`  
  
Especifica que debe recuperarse ese documento de hello otro origen definido por el alias de hello proporcionado.  
  
`<collection_expression> '.' property_`  
  
Especifica que debe recuperarse ese documento accediendo hello `property_name` especifica el elemento de matriz de propiedad o array_index para todos los documentos recuperados por expresión de colección.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Especifica que debe recuperarse ese documento accediendo hello `property_name` especifica el elemento de matriz de propiedad o array_index para todos los documentos recuperados por expresión de colección.  
  
**Comentarios**  
  
Todos los alias proporcionados o deducidos en hello `<from_source>(`s) deben ser únicos. Hola sintaxis `<collection_expression>.`property_name es Hola igual que `<collection_expression>' ['"property_name"']'`. Sin embargo, pueden utilizarse esta última sintaxis de hello si un nombre de propiedad contiene un carácter no son identificadores.  
  
**Manejo de situaciones en las que faltan propiedades o elementos de matriz o en las que hay valores sin definir**  
  
Si una expresión de colección accede a propiedades o elementos de matriz y el valor no existe, ese valor se omitirá y no se seguirá procesando.  
  
**Ámbito de contexto de la expresión de la colección**  
  
El ámbito de las expresiones de colección puede ser de colección o de documento:  
  
-   Una expresión es de ámbito de la colección, si hello origen subyacente de la expresión de colección de hello es ROOT o `collection_name`. Este tipo de expresión representa un conjunto de documentos directamente recuperados de la colección de hello directamente y no es dependiente del procesamiento de Hola de otras expresiones de la colección.  
  
-   Una expresión es de ámbito de documento, si hello origen subyacente de la expresión de colección de hello es `input_alias` presentada anteriormente en la consulta de Hola. Dicha expresión representa un conjunto de documentos obtenidos al evaluar la expresión de colección hello en el ámbito de Hola de cada documento que pertenece el conjunto de toohello asociado a la colección de alias de Hola.  conjunto resultante de Hello será una unión de los conjuntos obtenidos mediante la evaluación de expresión de colección de Hola para cada uno de los documentos de Hola Hola subyacente conjunto.  
  
**Combinaciones**  
  
En la versión actual de hello, base de datos de Azure Cosmos admite combinaciones internas. Las funcionalidades de combinación adicionales estarán disponibles próximamente.

Conjuntos de resultados de combinaciones internas en un producto cruzado completado de hello participan en la combinación de Hola. resultado de Hello de una combinación de N es un conjunto de tuplas de N elementos, donde cada valor de tupla Hola está asociado con un alias de hello establecer participan en la combinación de Hola y son accesibles mediante una referencia a ese alias en otras cláusulas.  
  
evaluación de saludo de combinación de hello depende de ámbito de contexto de Hola de hello participa conjuntos:  
  
-  La combinación entre un conjunto de ámbito de colección A y otro B da como resultado un producto cruzado de todos los elementos de los conjuntos A y B.
  
-   La combinación entre un conjunto A y un conjunto de ámbito de documento B da como resultado una unión de todos los conjuntos obtenidos de la evaluación de B para cada documento del conjunto A.  
  
 En la versión actual de hello, se admite un máximo de una expresión de ámbito de la colección por el procesador de consultas de Hola.  
  
**Ejemplos de combinaciones:**  
  
Echemos un vistazo a Hola siguiente cláusula FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Los orígenes definirán `input_alias1, input_alias2, …, input_aliasN`. Esta cláusula FROM devuelve un conjunto de N tuplas (tupla con N valores). Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección.  
  
*Ejemplo de COMBINACIÓN 1, con 2 orígenes:*  
  
- `<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.  
  
- `<from_source2>` tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:  
  
    {1, 2} para `input_alias1 = A,`  
  
    {3} para `input_alias1 = B,`  
  
    {4, 5} para `input_alias1 = C,`  
  
- Hola de cláusula `<from_source1> JOIN <from_source2>` dará como resultado Hola siguientes tuplas:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Ejemplo de COMBINACIÓN 2, con 3 orígenes:*  
  
- `<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.  
  
- `<from_source2>` tendrá ámbito de documento, hará referencia a `input_alias1` y representará los conjuntos:  
  
    {1, 2} para `input_alias1 = A,`  
  
    {3} para `input_alias1 = B,`  
  
    {4, 5} para `input_alias1 = C,`  
  
- `<from_source3>` tendrá ámbito de documento, hará referencia a `input_alias2` y representará los conjuntos:  
  
    {100, 200} para `input_alias2 = 1,`  
  
    {300} para `input_alias2 = 3,`  
  
- Hola de cláusula `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado Hola siguientes tuplas:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Falta de tuplas para otros valores de `input_alias1`, `input_alias2`, para qué hello `<from_source3>` no devolvió ningún valor.  
  
*Ejemplo de COMBINACIÓN 3, con 3 orígenes:*  
  
- <from_source1> tendrá ámbito de colección y representa el conjunto {A, B, C}.  
  
- `<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.  
  
- <from_source2> tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:  
  
    {1, 2} para `input_alias1 = A,`  
  
    {3} para `input_alias1 = B,`  
  
    {4, 5} para `input_alias1 = C,`  
  
- Permiten `<from_source3>` con demasiado el ámbito`input_alias1` y representa conjuntos:  
  
    {100, 200} para `input_alias2 = A,`  
  
    {300} para `input_alias2 = C,`  
  
- Hola de cláusula `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado Hola siguientes tuplas:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)  
  
> [!NOTE]
> Esto da como resultado un producto cruzado entre `<from_source2>` y `<from_source3>` porque ambos son toohello ámbito mismo `<from_source1>`.  Esto dio como resultado 4 (2 x 2) tuplas con valor A, 0 tuplas con valor B (1 x 0) y 2 (2 x 1) tuplas con valor C.  
  
**Consulte también**  
  
 [Cláusula SELECT](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> Cláusula WHERE  
 Especifica la condición de búsqueda de Hola para documentos de hello devuelto por la consulta de Hola.  
  
 **Sintaxis**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Argumentos**  
  
-   `<filter_condition>`  
  
     Especifica Hola condición toobe cumplido para hello documentos toobe devuelto.  
  
-   `<scalar_expression>`  
  
     Calcula la expresión que representa Hola valor toobe. Vea hello [expresiones escalares](#bk_scalar_expressions) sección para obtener más información.  
  
 **Comentarios**  
  
 En orden para hello toobe documento devuelve una expresión especificada como condición de filtro debe evaluarse tootrue. Solo un valor booleano true cumplirá la condición de hello, cualquier otro valor: sin definir, null, false, número, matriz u objeto no cumplirá la condición de Hola.  
  
##  <a name="bk_orderby_clause"></a> Cláusula ORDER BY  
 Especifica Hola orden de clasificación de resultados devueltos por la consulta de Hola.  
  
 **Sintaxis**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Argumentos**  
  
-   `<sort_specification>`  
  
     Especifica una propiedad o una expresión en la que del conjunto de resultados de consulta de hello toosort. Se puede especificar una columna de ordenación como alias de nombre o de columna.  
  
     Se pueden especificar varias columnas de ordenación. Los nombres de columna deben ser únicos. secuencia de Hola Hola de columnas de ordenación en la cláusula ORDER BY Hola define la organización de Hola Hola ordenado de conjunto de resultados. Es decir, conjunto de resultados de Hola se ordena por la primera propiedad de hello y, a continuación, esa lista ordenada se ordena por la segunda propiedad de Hola y así sucesivamente.  
  
     nombres de columna de Hello hace referencia en la cláusula ORDER BY Hola deben corresponderse tooeither una columna de hello seleccione lista o tooa columna definida en la tabla especificada en la cláusula FROM de hello sin ambigüedades.  
  
-   `<sort_expression>`  
  
     Especifica una propiedad única o una expresión en qué conjunto de resultados de consulta de hello toosort.  
  
-   `<scalar_expression>`  
  
     Vea hello [expresiones escalares](#bk_scalar_expressions) sección para obtener más información.  
  
-   `ASC | DESC`  
  
     Especifica que los valores de hello en la columna especificada de Hola se deben ordenar en orden ascendente o descendente. ASC ordena del valor de toohighest de valor más bajo de Hola. DESC ordena del valor de toolowest de valor más alto. ASC es el criterio de ordenación predeterminado de Hola. Valores NULL se tratan como valores de hello más bajos posibles.  
  
 **Comentarios**  
  
 Durante la gramática de consulta de hello permite varios pedidos por propiedades, tiempo de ejecución de consulta de base de datos de Azure Cosmos de hello admite ordenación únicamente en una sola propiedad y únicamente en los nombres de propiedad, es decir, no en las propiedades calculadas. Ordenar también requiere que Hola directiva de indexación incluye un índice de intervalo para la propiedad de Hola y Hola especificado tipo, con una precisión máxima de Hola. Consulte toohello documentación para obtener más detalles de la directiva de indización.  
  
##  <a name="bk_scalar_expressions"></a> Expresiones escalares  
 Una expresión escalar es una combinación de símbolos y operadores que se pueden evalúan tooobtain un valor único. Las expresiones simples pueden ser constantes, referencias de propiedad, referencias de elementos de matriz, referencias de alias o llamadas de función. Las expresiones simples se pueden combinar en expresiones complejas con operadores.  
  
 Para más información sobre los valores que puede tener una expresión escalar, consulte la sección [Constantes](#bk_constants).  
  
 **Sintaxis**  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 **Argumentos**  
  
-   `<constant>`  
  
     Representa un valor constante. Consulte la sección [Constantes](#bk_constants) para más información.  
  
-   `input_alias`  
  
     Representa un valor definido por hello `input_alias` introducidas en hello `FROM` cláusula.  
    Este valor se garantiza toonot ser **indefinido** :**indefinido** se omiten los valores de entrada de Hola.  
  
-   `<scalar_expression>.property_name`  
  
     Representa un valor de propiedad de Hola de un objeto. Si no existe ninguna propiedad de Hola o propiedad que se hace referencia en un valor que no es un objeto y luego Hola expresión, se evalúa como demasiado**indefinido** valor.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Representa un valor de propiedad de hello con nombre `property_name` o elemento de matriz con el índice `array_index` de una matriz de objetos. Si no existe el índice de propiedad o matriz de Hola o índice de la propiedad/matriz Hola se hace referencia en un valor que no es una matriz de objetos, a continuación, Hola expresión se evalúa como el valor de tooundefined.  
  
-   `unary_operator <scalar_expression>`  
  
     Representa un operador que sea tooa aplicado un solo valor. Consulte la sección [Operadores](#bk_operators) para más información.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Representa un operador que es tener valores tootwo aplicada. Consulte la sección [Operadores](#bk_operators) para más información.  
  
-   `<scalar_function_expression>`  
  
     Representa un valor definido por el resultado de una llamada de función.  
  
-   `udf_scalar_function`  
  
     Función escalar definida por el nombre de usuario de Hola.  
  
-   `builtin_scalar_function`  
  
     Nombre de función escalar integrada de Hola.  
  
-   `<create_object_expression>`  
  
     Representa un valor obtenido al crear un objeto con propiedades especificadas y sus valores.  
  
-   `<create_array_expression>`  
  
     Representa un valor obtenido al crear una matriz con valores especificados como elementos.  
  
-   `parameter_name`  
  
     Representa un valor de nombre de parámetro especificado de Hola. Nombres de parámetro deben tener un único @ como primer carácter de Hola.  
  
 **Comentarios**  
  
 Todos los argumentos deben estar definidos al llamar a una función escalar incorporada o definida por el usuario. Si alguno de los argumentos de hello no está definido, no se llamará función hello y Hola resultado será indefinido.  
  
 Cuando se crea un objeto, cualquier propiedad que se asigna el valor no definido se omite y no se incluyen en hello creado el objeto.  
  
 Cuando se asigna la creación de una matriz, cualquier valor del elemento que **indefinido** valor se omite y no se incluyen en el objeto Hola creado. Esto hará que tootake de elemento de Hola a continuación definida su lugar como dicha matriz Hola creado no tenga índices omitidos.  
  
##  <a name="bk_operators"></a> Operadores  
 Esta sección describe los operadores de hello compatible. Cada operador puede ser tooexactly asignado una categoría.  
  
 Consulte la siguiente tabla, **Categorías de operadores**, para más información acerca del control de los valores **undefined**, los requisitos de tipo de valores de entrada y el control de los valores con tipos no coincidentes.  
  
 **Categorías de operadores:**  
  
|**Categoría**|**Detalles**|  
|-|-|  
|**aritméticos**|El operador espera que las entradas toobe números. La salida también es un número. Si se cumple alguna de las entradas de hello **indefinido** o es de tipo que no sea resultado de número, a continuación, hello **indefinido**.|  
|**bit a bit**|El operador espera que las entradas entero con signo de 32 bits de toobe números. La salida también es un número entero con signo de 32 bits.<br /><br /> Los valores que no sean enteros se redondean. Los valores positivos se redondean a la baja y los negativos, a la alta.<br /><br /> Se convertirá cualquier valor que está fuera del intervalo de entero de 32 bits de hello, aprovechando los últimos 32 bits de sus dos notaciones de complementos.<br /><br /> Si se cumple alguna de las entradas de hello **indefinido** o tipo que no sea número, entonces el resultado de hello es **indefinido**.<br /><br /> **Nota:** Hola anteriormente el comportamiento es compatible con el comportamiento del operador bit a bit de JavaScript.|  
|**lógicos**|El operador espera que las entradas toobe booleanas. La salida también es un booleano.<br />Si se cumple alguna de las entradas de hello **indefinido** o tipo que no sea un valor booleano, será el resultado de hello **indefinido**.|  
|**de comparación**|El operador espera que las entradas toohave Hola mismo tipo y no sean sin definir. La salida es un booleano.<br /><br /> Si se cumple alguna de las entradas de hello **indefinido** u Hola entradas tienen tipos diferentes, el resultado de hello es **indefinido**.<br /><br /> Consulte la tabla **Ordenación de los valores para la comparación** para conocer los detalles de ordenación de los valores.|  
|**cadena**|El operador espera que las entradas toobe cadenas. La salida también es una cadena.<br />Si se cumple alguna de las entradas de hello **indefinido** o es de tipo que no sea resultado de cadena, a continuación, hello **indefinido**.|  
  
 **Operadores unarios:**  
  
|**Name**|**Operador**|**Detalles**|  
|-|-|-|  
|**aritméticos**|+<br /><br /> -|Devuelve el valor número Hola.<br /><br /> Negativos bit a bit. Devuelve el valor numérico negativo.|  
|**bit a bit**|~|Complemento de uno. Devuelve un complemento de un valor numérico.|  
|**lógicos**|**NOT**|Negación. Devuelve el valor booleano negativo.|  
  
 **Operadores binarios:**  
  
|**Name**|**Operador**|**Detalles**|  
|-|-|-|  
|**aritméticos**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Suma.<br /><br /> Resta.<br /><br /> Multiplicación.<br /><br /> División.<br /><br /> Modulación.|  
|**bit a bit**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|OR bit a bit.<br /><br /> AND bit a bit.<br /><br /> XOR bit a bit.<br /><br /> Desplazamiento a la izquierda.<br /><br /> Desplazamiento a la derecha.<br /><br /> Desplazamiento a la derecha con relleno de ceros.|  
|**lógicos**|**AND**<br /><br /> **O bien**|Conjunción lógica. Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.<br /><br /> Conjunción lógica. Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.|  
|**de comparación**|**=**<br /><br /> **!=, &lt;&gt;**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Igual a. Devuelve **true** si ambos argumentos son iguales, en caso contrario, devuelve **false**.<br /><br /> Diferente de. Devuelve **true** si ambos argumentos no son iguales, en caso contrario, devuelve **false**.<br /><br /> Mayor que. Devuelve **true** si el primer argumento es mayor que otra de Hola, devolver **false** en caso contrario.<br /><br /> Mayor o igual que. Devuelve **true** si el primer argumento es mayor o igual a otra toohello, devolver **false** en caso contrario.<br /><br /> Menor que. Devuelve **true** si el primer argumento es menor que otra de Hola, devolver **false** en caso contrario.<br /><br /> Menor o igual que. Devuelve **true** si el primer argumento es menor o igual toohello segundo uno, devuelto **false** en caso contrario.<br /><br /> Fusionar. Devuelve Hola segundo argumento si Hola primer argumento es un **indefinido** valor.|  
|**String**|**&amp;#124;&amp;#124;**|Concatenación. Devuelve una concatenación de ambos argumentos.|  
  
 **Operadores ternarios:**  
  
|Operador ternario|?|Devuelve Hola segundo argumento si Hola primer argumento se evalúa demasiado**true**; devuelve el tercer argumento de hello en caso contrario.|  
|-|-|-|  
  
 **Ordenación de los valores para la comparación**  
  
|**Tipo**|**Orden de los valores**|  
|-|-|  
|**Undefined**|No comparables.|  
|**Null**|Valor único: **null**|  
|**Number**|Número real natural.<br /><br /> El valor de infinito negativo es menor que cualquier otro valor numérico.<br /><br /> El valor de infinito positivo es mayor que cualquier otro valor numérico. El valor **NaN** no es comparable. La comparación con **NaN** dará como resultado el valor **undefined**.|  
|**String**|Orden lexicográfico.|  
|**Array**|Ningún orden, pero equitativo.|  
|**Object**|Ningún orden, pero equitativo.|  
  
 **Comentarios**  
  
 En la base de datos de Azure Cosmos, tipos de Hola de valores a menudo no se conocen hasta que realmente se recuperan de la base de datos de Hola. En orden toosupport una ejecución eficaz de las consultas, la mayoría de los operadores de hello tiene estrictos requisitos de tipos. Además, los operadores por sí mismos no realizan conversiones implícitas.  
  
 Esto significa que una consulta como: seleccione * FROM ROOT r WHERE r.Age = 21 solo devolverá documentos con la propiedad Age igual toohello número 21. Documentos con la propiedad Age igual toohello cadena "21" u Hola "0021" no coincidirán, como expresión de Hola "21" = 21 se evalúa como tooundefined. Esto permite un mejor uso de índices, porque búsqueda Hola de un valor específico (es decir, el número 21) es más rápido que busque un número indefinido de coincidencias posibles (es decir, el número 21 o las cadenas "21", "021", "21.0"...). Esto difiere de la evaluación de los distintos tipos de valores de los operadores en JavaScript.  
  
 **Comparación e igualdad de objetos y matrices**  
  
 La comparación de valores de Array u Object mediante los operadores de intervalo (>, > =, <, < =) dará como resultado undefined, ya que no hay orden definido en los valores de Object o Array. Sin embargo, se admite con operadores de igualdad y desigualdad (=,! =, <>) y los valores se compararán estructuralmente.  
  
 Las matrices son iguales si ambas tienen el mismo número de elementos y los elementos de las posiciones coincidentes también son iguales. Si compara cualquier par de elementos da como resultado sin definir, resultado de hello de comparación de la matriz es indefinido.  
  
 Los objetos son iguales si tienen las mismas propiedades definidas y si los valores de las propiedades coincidentes también son iguales. Si compara cualquier par de valores de propiedad da como resultado sin definir, resultado de hello de comparación de objetos es indefinido.  
  
##  <a name="bk_constants"></a> Constantes  
 Una constante, también conocida como valor literal o escalar, es un símbolo que representa un valor de datos específicos. formato de Hola de una constante depende de tipo de datos de hello del valor de Hola que representa.  
  
 **Tipos de datos escalares admitidos:**  
  
|**Tipo**|**Orden de los valores**|  
|-|-|  
|**Undefined**|Valor único: **undefined**|  
|**Null**|Valor único: **null**|  
|**Boolean**|Valores: **false**, **true**.|  
|**Number**|Número de punto flotante de precisión doble, estándar IEEE 754.|  
|**String**|Secuencia de cero o más caracteres Unicode. Las cadenas deben ir entre comillas sencillas o dobles.|  
|**Array**|Secuencia de cero o más elementos. Cada elemento puede ser un valor de cualquier tipo de datos escalar, excepto Undefined.|  
|**Object**|Conjunto desordenado de cero o más pares nombre/valor. Nombre es una cadena Unicode, el valor puede ser de cualquier tipo de datos escalar, excepto **Undefined**.|  
  
 **Sintaxis**  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 **Argumentos**  
  
1.  `<undefined_constant>; undefined`  
  
     Representa un valor sin definir de tipo Undefined.  
  
2.  `<null_constant>; null`  
  
     Representa el valor **null** de tipo **Null**.  
  
3.  `<boolean_constant>`  
  
     Representa la constante de tipo booleano.  
  
4.  `false`  
  
     Representa el valor **false** de tipo booleano.  
  
5.  `true`  
  
     Representa el valor **true** de tipo booleano.  
  
6.  `<number_constant>`  
  
     Representa una constante.  
  
7.  `decimal_literal`  
  
     Los literales decimales son números representados mediante notación decimal o científica.  
  
8.  `hexadecimal_literal`  
  
     Los literales hexadecimales son números representados mediante el prefijo "0x-" seguido de uno o más dígitos hexadecimales.  
  
9. `<string_constant>`  
  
     Representa una constante de tipo cadena.  
  
10. `string _literal`  
  
     Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape. Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: ").  
  
 Se permiten las secuencias de escape siguientes:  
  
|**Secuencia de escape**|**Descripción**|**Carácter Unicode**|  
|-|-|-|  
|\\'|apóstrofo (')|U + 0027|  
|\\"|comillas dobles (")|U + 0022|  
|\\\|barra inclinada inversa (\\)|U + 005C|  
|\\/|barra inclinada (/)|U + 002F|  
|\b|retroceso|U + 0008|  
|\f|avance de página|U + 000C|  
|\n|avance de línea|U + 000A|  
|\r|retorno de carro|U + 000D|  
|\t|tabulador|U + 0009|  
|\uXXXX|Carácter Unicode definidos por 4 dígitos hexadecimales.|U + XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a> Guías de rendimiento de las consultas  
 En orden para un toobe consulta ejecutado eficazmente para una colección de gran tamaño, debe utilizar filtros que pueden obtenerse a través de uno o más índices.  
  
 Hola después de filtros se considerará de búsqueda del índice:  
  
-   Utilice el operador de igualdad (=) con expresiones de ruta de acceso de documentos y constantes.  
  
-   Utilice los operadores de intervalo (<, \<=, >, >=) con expresiones de ruta de acceso de documentos y constantes numéricas.  
  
-   Expresión de ruta de acceso de documento indica cualquier expresión que identifica una ruta de acceso constante en documentos de Hola de colección de la base de datos de hello al que hace referencia.  
  
 **Expresión de ruta de acceso de documento**  
  
 Las expresiones de ruta de acceso de documento son expresiones que evalúan la ruta de una propiedad o un indexador de matrices en un documento procedente de la colección de bases de datos. Esta ruta de acceso puede ser usado tooidentify Hola ubicación de valores que se hace referencia en un filtro directamente dentro de los documentos de hello en la colección de la base de datos de Hola.  
  
 Para que una expresión toobe considera una expresión de ruta de acceso del documento, debe:  
  
1.  Referencia Hola raíz directamente.  
  
2.  Hacer referencia al indexador de matrices de propiedad o constantes de alguna expresión de ruta de acceso de documento.  
  
3.  Hacer referencia a un alias, que represente alguna expresión de ruta de acceso de documento.  
  
     **Convenciones de sintaxis**  
  
     Hello en la tabla siguiente describe la sintaxis de toodescribe de hello convenciones utilizadas en la referencia del lenguaje de consulta de API de documentos Hola.  
  
    |**Convención**|**Se usa para**|  
    |-|-|    
    |MAYÚSCULAS|Palabras clave sin distinción entre mayúsculas y minúsculas.|  
    |minúsculas|Palabras clave con distinción entre mayúsculas y minúsculas.|  
    |\<noterminal&gt;|Elemento no terminal, se define por separado.|  
    |\<noterminal&gt; ::=|Definición de la sintaxis de elemento no Terminal de Hola.|  
    |otro_terminal|Terminal (token), se describe detalladamente en palabras.|  
    |identificador|Identificador. Solo admite los caracteres siguientes:, a-z, A-Z, 0-9 _El primer carácter no puede ser un dígito.|  
    |"cadena"|Cadena entrecomillada. Permite cualquier cadena válida. Vea la descripción de string_literal.|  
    |'símbolo'|Símbolo literal que forma parte de la sintaxis de Hola.|  
    |&#124; (barra vertical)|Alternativas para los elementos de la sintaxis. Puede usar solo uno de los elementos de hello especificados.|  
    |[] /(corchetes)|Los corchetes contienen uno o varios elementos opcionales.|  
    |[, ...n]|Indica Hola anterior elemento se puede repetir n número de veces. Hola elementos se separan por comas.|  
    |[ ...n]|Indica Hola anterior elemento se puede repetir n número de veces. elementos de Hola se separan mediante espacios en blanco.|  
  
##  <a name="bk_built_in_functions"></a> Funciones integradas  
 Azure Cosmos DB proporciona muchas funciones de SQL integradas. categorías de Hola de funciones integradas se enumeran a continuación.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Funciones matemáticas](#bk_mathematical_functions)|Hola funciones matemáticas cada realizan un cálculo, normalmente basado en valores de entrada que se proporcionan como argumentos y devuelven un valor numérico.|  
|[Funciones de comprobación de tipos](#bk_type_checking_functions)|funciones de comprobación de tipo Hello permiten a tipo de hello toocheck de una expresión dentro de las consultas SQL.|  
|[Funciones de cadena](#bk_string_functions)|funciones de cadena de Hello realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano.|  
|[Funciones de matriz](#bk_array_functions)|funciones de matriz de Hello realizan una operación en un valor de matriz de entrada y devuelven numérico, un valor booleano o de matriz.|  
|[Funciones espaciales](#bk_spatial_functions)|funciones espaciales Hola realizan una operación sobre un valor de entrada de objeto espacial y devuelven un valor numérico o booleano.|  
  
###  <a name="bk_mathematical_functions"></a> Funciones matemáticas  
 Hello siguientes funciones realizan un cálculo, normalmente basado en valores de entrada que se proporcionan como argumentos y devuelven un valor numérico.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DEGREES](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOG](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[POWER](#bk_power)|  
|[RADIANS](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[SQUARE](#bk_square)|[SIGN](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica.  
  
 **Sintaxis**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se muestra los resultados de Hola de usar la función hello ABS en tres números distintos.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 Ángulo de hello devuelve, en radianes, cuyo coseno es Hola expresión numérica especificada; También se denomina arco coseno.  
  
 **Sintaxis**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola ACOS de -1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 Ángulo de hello devuelve, en radianes, cuyo seno es hello especifica expresión numérica. También se denomina arcoseno.  
  
 **Sintaxis**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola ASIN de -1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 Ángulo de hello devuelve, en radianes, cuya tangente es hello especifica expresión numérica. También se denomina arcotangente.  
  
 **Sintaxis**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo devuelve Hola ATAN de hello valor especificado.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 Devuelve el valor de entidad de seguridad de Hola de hello arco tangente de y/x x, expresado en radianes.  
  
 **Sintaxis**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se calcula hello ATN2 para hello especificado x e y componentes.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada.  
  
 **Sintaxis**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo muestra numéricos positivos, negativos y valores cero con Hola función CEILING.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 Devuelve Hola coseno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.  
  
 **Sintaxis**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo calcula Hola COS de hello especifica el ángulo.  
  
```  
SELECT COS(14.78)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 Devuelve Hola cotangente trigonométrica Hola especifica el ángulo, en radianes, en hello especifica la expresión numérica.  
  
 **Sintaxis**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo calcula Hola COT del ángulo especificado Hola.  
  
```  
SELECT COT(124.1332)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 Devuelve Hola ángulo correspondiente en grados para un ángulo especificado en radianes.  
  
 **Sintaxis**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola número de grados en un ángulo de PI/2 radianes.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica.  
  
 **Sintaxis**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo muestra numéricos positivos, negativos y cero valores con Hola FLOOR (función).  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 Devuelve Hola valor exponencial de hello especifica la expresión numérica.  
  
 **Sintaxis**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Comentarios**  
  
 constante de Hello **e** (2,718281 …) es Hola base de los logaritmos naturales.  
  
 Hello exponente de un número es constante de hello **e** genera potencia de toohello de número de Hola. Por ejemplo EXP(1,0) = e^1,0 = 2,718 281 828 459 05 y EXP(10) = e^10 = 22 026,465 794 806 7.  
  
 Hola valor exponencial del logaritmo natural de Hola de un número es el número de hello propio: EXP (LOG (n)) = n. Logaritmo natural de Hola de hello exponencial de un número es el número de hello propio: LOG (EXP (n)) = n.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se declara una variable y devuelve el valor exponencial de saludo de la variable especificada de hello (10).  
  
```  
SELECT EXP(10)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Hello en el ejemplo siguiente se devuelve Hola valor exponencial del logaritmo natural de Hola de 20 y el logaritmo natural de Hola de hello exponencial de 20. Dado que estas funciones son funciones inversas entre sí, valor devuelto de hello con redondeo para matemáticas en ambos casos son 20 de punto flotante.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 Devuelve el logaritmo de natural de Hola de hello especificado expresión numérica.  
  
 **Sintaxis**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
-   `base`  
  
     Argumento numérico opcional que establece base logaritmo Hola Hola.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Comentarios**  
  
 De forma predeterminada, LOG() devuelve el logaritmo natural de Hola. Puede cambiar Hola base del valor de hello logaritmo tooanother mediante el uso del parámetro base opcional Hola.  
  
 logaritmo natural de Hello es Hola logaritmo toohello base **e**, donde **e** es un too2.718281828 aproximadamente igual constante irracional.  
  
 logaritmo natural de Hola de hello exponencial de un número es el número de hello propio: LOG (EXP (n)) = n. Hola valor exponencial del logaritmo natural de Hola de un número es el número de hello propio: EXP (LOG (n)) = n.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se declara una variable y devuelve Hola logaritmo valor de la variable especificada de hello (10).  
  
```  
SELECT LOG(10)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Hello en el ejemplo siguiente se calcula Hola registro exponente Hola de un número.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 Devuelve el logaritmo de base 10 de Hola de hello especifica la expresión numérica.  
  
 **Sintaxis**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Comentarios**  
  
 Hola LOG10 y funciones POWER están relacionada inversamente tooone otro. Por ejemplo, 10 ^ LOG10 (n) = n.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se declara una variable y devuelve Hola LOG10 valor de la variable especificada de hello (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 Devuelve Hola valor constante de PI.  
  
 **Sintaxis**  
  
```  
PI ()  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve el valor de Hola de PI.  
  
```  
SELECT PI()  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 Devuelve Hola valo Hola especificado expresión toohello potencia especificada.  
  
 **Sintaxis**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
-   `y`  
  
     Es Hola power toowhich tooraise `numeric_expression`.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente se muestra cómo elevar números toohello potencia de 3 (Hola cubo del número de hello).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 Devuelve radianes cuando se especifica una expresión numérica en grados.  
  
 **Sintaxis**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se toma unos ángulos como entrada y devuelve sus correspondientes valores en radianes.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 Devuelve un valor numérico, redondeado toohello valor de entero más cercano.  
  
 **Sintaxis**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se redondea Hola después toohello números positivos y negativos al entero más próximo.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 Devuelve Hola positivo (+ 1), cero (0), o signo negativo (-1) de hello especificado expresión numérica.  
  
 **Sintaxis**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve valores de inicio de sesión de Hola de números de-2 too2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 Devuelve Hola seno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.  
  
 **Sintaxis**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo calcula Hola seno del ángulo especificado Hola.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 Devuelve Hola cuadrado raíz de hello especifica el valor numérico.  
  
 **Sintaxis**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve raíces cuadradas de Hola de números 1 a 3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 Hola devuelve cuadrado de hello especifica el valor numérico.  
  
 **Sintaxis**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve cuadrados Hola de números 1 a 3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Tangente de hello devuelve de hello especifica el ángulo, en radianes, en hello expresión especificada.  
  
 **Sintaxis**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se calcula tangente de Hola de PI () / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> TRUNC  
 Devuelve un valor numérico, el valor entero más cercano de toohello truncado.  
  
 **Sintaxis**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     Es una expresión numérica.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente trunca Hola siguientes números positivos y negativos toohello valor entero más cercano.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> Funciones de comprobación de tipos  
 Hello siguientes funciones admiten la comprobación de tipos contra valores de entrada y devuelven un valor booleano.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> IS_ARRAY  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una matriz.  
  
 **Sintaxis**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_ARRAY.  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> IS_BOOL  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un valor booleano.  
  
 **Sintaxis**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_BOOL.  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> IS_DEFINED  
 Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor.  
  
 **Sintaxis**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hola siguiendo en el ejemplo se comprueba presencia de Hola de una propiedad dentro de hello había especificado documento JSON. Hola primero devuelve true, ya que "a" está presente, pero Hola segundo devuelve false porque "b" no está presente.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> IS_NULL  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es null.  
  
 **Sintaxis**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_NULL.  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> IS_NUMBER  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un número.  
  
 **Sintaxis**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_NULL.  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> IS_OBJECT  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un objeto JSON.  
  
 **Sintaxis**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_OBJECT.  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> IS_PRIMITIVE  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un tipo primitivo (cadena, booleano, numérico o null).  
  
 **Sintaxis**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_PRIMITIVE.  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una cadena.  
  
 **Sintaxis**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_STRING.  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> Funciones de cadena  
 Hola siguientes funciones escalares realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LEFT](#bk_left)|[LENGTH](#bk_length)|  
|[LOWER](#bk_lower)|[LTRIM](#bk_ltrim)|[REPLACE](#bk_replace)|  
|[REPLICATE](#bk_replicate)|[REVERSE](#bk_reverse)|[RIGHT](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[UPPER](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena.  
  
 **Sintaxis**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola siguiendo en el ejemplo se devuelve una cadena concatenada de Hola de hello valores especificados.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar.  
  
 **Sintaxis**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se comprueba si "abc" contiene "ab" y contiene "d".  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar.  
  
 **Sintaxis**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola "abc" termina con "b" y "bc".  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> INDEX_OF  
 Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola.  
  
 **Sintaxis**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve el índice de Hola de varias subcadenas dentro de "abc".  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> LEFT  
 Devuelve Hola parte izquierda de una cadena con hello especificada número de caracteres.  
  
 **Sintaxis**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
-   `num_expr`  
  
     Es cualquier expresión numérica válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola izquierda de "abc" para distintos valores de longitud.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> LENGTH  
 Devuelve el número de caracteres de Hola Hola especificado expresión de cadena.  
  
 **Sintaxis**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola longitud de una cadena.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas.  
  
 **Sintaxis**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toouse inferior en una consulta.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales.  
  
 **Sintaxis**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toouse LTRIM dentro de una consulta.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> REPLACE  
 Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena.  
  
 **Sintaxis**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente muestra cómo reemplazar el toouse en una consulta.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 Repite un valor de cadena un número especificado de veces.  
  
 **Sintaxis**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
-   `num_expr`  
  
     Es cualquier expresión numérica válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente muestra cómo REPLICAR toouse en una consulta.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 Devuelve Hola invirtiendo el orden de un valor de cadena.  
  
 **Sintaxis**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente muestra cómo toouse INVERTIR en una consulta.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 Hola devuelve parte derecha de una cadena con hello del número de caracteres especificado.  
  
 **Sintaxis**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
-   `num_expr`  
  
     Es cualquier expresión numérica válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola la parte derecha de "abc" para distintos valores de longitud.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 Devuelve una expresión de cadena después de quitar los espacios en blanco finales.  
  
 **Sintaxis**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toouse RTRIM dentro de una consulta.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 Devuelve un valor booleano que indica si primera expresión de cadena Hola empieza por hello en segundo lugar.  
  
 **Sintaxis**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hello el ejemplo siguiente se comprueba si hello cadena "abc" comienza con "b" y "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Devuelve parte de una expresión de cadena a partir de hello especifica la posición de base cero del carácter y continúa toohello especifica la longitud o toohello final de cadena de Hola.  
  
 **Sintaxis**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
-   `num_expr`  
  
     Es cualquier expresión numérica válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hello en el ejemplo siguiente se devuelve Hola subcadena de "abc" comienza en 1 y una longitud de 1 carácter.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula.  
  
 **Sintaxis**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     Es cualquier expresión de cadena válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de cadena.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toouse superior en una consulta  
  
```  
SELECT UPPER("Abc")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> Funciones de matriz  
 Hola siguientes funciones escalares realiza una operación sobre un valor de entrada de matriz y devolución numérico, booleano o matriz.  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> ARRAY_CONCAT  
 Devuelve una matriz que es el resultado de hello de concatenar dos o más valores de la matriz.  
  
 **Sintaxis**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     Es cualquier expresión de matriz válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión de matriz.  
  
 **Ejemplos**  
  
 Hola después ejemplo cómo tooconcatenate dos matrices.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> ARRAY_CONTAINS  
 Devuelve un valor booleano que indica si la matriz de hello contiene Hola valor especificado.  
  
 **Sintaxis**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     Es cualquier expresión de matriz válida.  
  
-   `expr`  
  
     Es cualquier expresión válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve un valor booleano.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo de cómo toocheck pertenencia a una matriz usar ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a> ARRAY_LENGTH  
 Devuelve el número de elementos de Hola Hola especifica la expresión de matriz.  
  
 **Sintaxis**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     Es cualquier expresión de matriz válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica.  
  
 **Ejemplos**  
  
 Hola después ejemplo cómo tooget Hola longitud de una matriz usar ARRAY_LENGTH.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> ARRAY_SLICE  
 Devuelve parte de una expresión de matriz.
  
 **Sintaxis**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     Es cualquier expresión de matriz válida.  
  
-   `num_expr`  
  
     Es cualquier expresión numérica válida.  
  
 **Tipos de valor devuelto**  
  
 Devuelve un valor booleano.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo de cómo tooget una parte de una matriz usar ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> Funciones espaciales  
 Hola siguientes funciones escalares realizan una operación sobre un valor de entrada de objeto espacial y devuelven un valor numérico o booleano.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.  
  
 **Sintaxis**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión numérica que contiene la distancia de Hola. Esto se expresa en metros Hola predeterminado sistema de referencia.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo tooreturn todos los documentos de familia que están dentro de 30 km de hello especificado ubicación mediante la función integrada de hello ST_DISTANCE. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 Devuelve una expresión booleana que indica si hello GeoJSON el objeto (punto, polígono o LineString) especificado en el primer argumento de hello es dentro de hello GeoJSON (punto, polígono o LineString) en el segundo argumento de Hola.  
  
 **Sintaxis**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
 
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
  
 **Tipos de valor devuelto**  
  
 Devuelve un valor booleano.  
  
 **Ejemplos**  
  
 Hola de ejemplo siguiente muestra cómo toofind familia de todos los documentos dentro de un polígono con ST_WITHIN.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> ST_INTERSECTS  
 Devuelve una expresión booleana que indica si el objeto de la GeoJSON de hello (punto, polígono o LineString) especificado en el primer argumento de hello superpuesto hello GeoJSON (punto, polígono o LineString) en el segundo argumento de Hola.  
  
 **Sintaxis**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
 
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
  
 **Tipos de valor devuelto**  
  
 Devuelve un valor booleano.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toofind todas las áreas que forma una intersección con Hola especificado polígono.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.  
  
 **Sintaxis**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.  
  
 **Tipos de valor devuelto**  
  
 Devuelve una expresión condicional.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo se muestra cómo toocheck si un punto es válido utilizando ST_VALID.  
  
 Por ejemplo, este punto tiene un valor de latitud que no está en el intervalo válido de Hola de valores [-90, 90], Hola por lo que la consulta devuelve false.  
  
 Para los polígonos, hello GeoJSON especificación requiere que debe ser proporcionado de par de coordenadas última Hola Hola igual como hello en primer lugar, toocreate una forma cerrada. El orden de los puntos dentro de un polígono debe especificarse siguiendo el sentido contrario al de las agujas del reloj. Un polígono especificado en el orden de las agujas del reloj representa inverso de Hola de región de hello dentro de él.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.  
  
 **Sintaxis**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     Es cualquier expresión válida de objeto Point o Polygon de GeoJSON.  
  
 **Tipos de valor devuelto**  
  
 Devuelve un valor JSON que contiene un valor booleano si Hola especifica el punto de GeoJSON o expresión de polígono es válida y, si no es válido, además Hola motivo como un valor de cadena.  
  
 **Ejemplos**  
  
 Hola siguiente ejemplo de cómo toocheck validez (con detalles) mediante ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Este es el conjunto de resultados de Hola.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Sintaxis SQL y consulta SQL para Azure Cosmos DB](documentdb-sql-query.md)   
 [Documentación sobre Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
