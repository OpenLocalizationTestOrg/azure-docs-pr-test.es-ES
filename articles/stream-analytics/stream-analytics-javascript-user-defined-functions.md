---
title: "funciones definidas por el usuario de JavaScript de análisis de transmisiones aaaAzure | Documentos de Microsoft"
description: "Realizar mecánica de consultas avanzadas con funciones definidas por el usuario en JavaScript"
keywords: javascript, funciones definidas por el usuario, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Funciones definidas por el usuario en JavaScript para Azure Stream Analytics
Azure Stream Analytics admite funciones definidas por el usuario escritas en JavaScript. Conjunto completo de Hola de **cadena**, **RegExp**, **matemáticas**, **matriz**, y **fecha** métodos que JavaScript proporciona, las transformaciones de datos complejos con trabajos de análisis de transmisiones se convierten en toocreate más fácil.

## <a name="javascript-user-defined-functions"></a>Funciones definidas por el usuario en JavaScript
Las funciones definidas por el usuario en JavaScript admiten funciones escalares de solo cálculo y sin estado, que no requieren conectividad externa. Hola devuelve el valor de una función sólo puede ser un valor escalar (único). Después de agregar un trabajo de tooa de función definida por el usuario de JavaScript, puede utilizar función hello en cualquier parte en la consulta de hello, como una función escalar integrada.

Estos son algunos escenarios en los que le podrían resultar útiles las funciones definidas por el usuario en JavaScript:
* Análisis y manipulación de cadenas que incluyen funciones de expresiones regulares, por ejemplo, **Regexp_Replace()** y **Regexp_Extract()**
* Descodificación y codificación de datos, por ejemplo, conversión de binario a hexadecimal
* Realización de cálculos matemáticos con funciones **matemáticas** de JavaScript
* Realización de operaciones de matriz como ordenar, combinar, buscar y rellenar

Aquí se indican algunas operaciones que no se pueden realizar con una función definida por el usuario de JavaScript en Stream Analytics:
* Llamar a puntos de conexión de REST externos, por ejemplo, mediante la realización de una búsqueda inversa de direcciones IP o una extracción de datos de referencia de un origen externo
* Realizar la serialización o deserialización de formatos de eventos personalizados en entradas y salidas
* Crear agregados personalizados

Aunque las funciones como **Date.GetDate()** o **Math.random()** no están bloqueados en la definición de funciones de hello, debería evitar su uso. Estas funciones **no** devuelto Hola mismo resultado cada vez que llamarlas y Hola servicio Azure Stream Analytics no mantiene un diario de las llamadas a funciones y devuelve resultados. Si una función devuelve un resultado diferente en hello mismos eventos, repetibilidad no se garantiza que cuando se reinicia un trabajo por usted o por el servicio de análisis de transmisiones de Hola.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Agregar una función definida por el usuario de JavaScript en hello portal de Azure
toocreate una función definida por el usuario simple de JavaScript en un trabajo de análisis de transmisiones existente, siga estos pasos:

1.  En hello portal de Azure, busque el trabajo de análisis de transmisiones.
2.  En **TOPOLOGÍA DE TRABAJO**, seleccione la función. Aparece una lista vacía de funciones.
3.  toocreate una nueva función definida por el usuario, seleccione **agregar**.
4.  En hello **nueva función** hoja, para **tipo de función**, seleccione **JavaScript**. Una plantilla de función predeterminado aparece en el editor de Hola.
5.  Para hello **alias UDF**, escriba **hex2Int**y cambiar la implementación de la función de hello como sigue:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Seleccione **Guardar**. La función aparece en la lista de Hola de funciones.
7.  Seleccione Hola de nuevo **hex2Int** función y comprobar la definición de función de Hola. Todas las funciones tienen un **UDF** alias de prefijo de función de agregado toohello. Necesita demasiado*incluir el prefijo de hello* cuando se llama a función hello en la consulta de análisis de transmisiones. En este caso, debe llamar a **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Llamada a una función definida por el usuario de JavaScript en una consulta

1. Hola editor de consultas, en **trabajo topología**, seleccione **consulta**.
2.  Editar la consulta y, a continuación, llame a función definida por el usuario de hello, similar al siguiente:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  archivo de datos de ejemplo de Hola tooupload, entrada de trabajo de Hola de menú contextual.
4.  tootest la consulta, seleccione **prueba**.


## <a name="supported-javascript-objects"></a>Objetos de JavaScript compatibles
Las funciones definidas por el usuario en JavaScript para Azure Stream Analytics admiten objetos de JavaScript estándar e integrados. Para obtener una lista de estos objetos, consulte [Objetos globales](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Conversión de tipos de Stream Analytics y JavaScript

Existen diferencias en los tipos de Hola que admiten el lenguaje de consultas de análisis de transmisiones de Hola y JavaScript. Esta tabla enumeran las asignaciones de conversión de hello entre Hola dos:

Stream Analytics | JavaScript
--- | ---
bigint | Número (JavaScript solo puede representar enteros seguridad tooprecisely 2 ^ 53)
DateTime | Date (JavaScript solo admite milisegundos)
double | Number
nvarchar(MAX) | String
Registro | Objeto
Matriz | Matriz
NULL | Null


Estas son las conversiones de JavaScript a Stream Analytics:


JavaScript | Stream Analytics
--- | ---
Number | Bigint (si el número de hello es round y entre larga. MinValue y long. MaxValue; en caso contrario, es double)
Date | DateTime
String | nvarchar(MAX)
Objeto | Registro
Matriz | Matriz
Null, sin definir | NULL
Cualquier otro tipo (por ejemplo, una función o un error) | No admitido (da lugar a un error en tiempo de ejecución)

## <a name="troubleshooting"></a>Solución de problemas
Errores de tiempo de ejecución de JavaScript se consideran muy negativos y se exponen a través del registro de actividad de Hola. registro de hello tooretrieve, expresada en hello portal de Azure, vaya tooyour trabajo y seleccione **registro de actividad**.


## <a name="other-javascript-user-defined-function-patterns"></a>Otros patrones de función definida por el usuario de JavaScript

### <a name="write-nested-json-toooutput"></a>Escribir anidada toooutput JSON
Si tiene un paso del procesamiento de seguimiento que utiliza un trabajo de análisis de transmisiones de salida como entrada, y requiere un formato JSON, puede escribir una toooutput de cadena JSON. el ejemplo siguiente se Hola llama hello **JSON.stringify()** toopack todos los pares de nombre/valor de hello de entrada y, a continuación, escriben como un único valor de cadena en la salida de función.

**Definición de funciones definidas por el usuario en JavaScript:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Consulta de ejemplo:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
