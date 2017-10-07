---
title: "búsquedas de registro aaaRegular las expresiones de análisis de registros de OMS | Documentos de Microsoft"
description: "Puede usar la palabra clave de RegEx hello en análisis de registros registro búsquedas toohello Hola resultados del filtro según la expresión regular tooa.  Este artículo proporciona la sintaxis de Hola para estas expresiones con varios ejemplos."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Mediante expresiones regulares toofilter busca registros de análisis de registros

[Búsquedas de registro](log-analytics-log-searches.md) permiten tooextract información del repositorio de análisis de registros de Hola.  [Expresiones de filtro](log-analytics-search-reference.md#filter-expressions) permitir resultados de hello toofilter de búsqueda de hello según criterios de toospecific.  Hola **RegEx** palabra clave permite toospecify una expresión regular para este filtro.  

Este artículo proporciona detalles acerca de la sintaxis de expresión regular de hello utilizado por el análisis de registros.

> [!NOTE]
> Solo puede utilizar expresiones regulares con campos de búsqueda.  Para más información sobre los campos de búsqueda, consulte **Tipos de campo** en [Descripción de las búsquedas de registros en Log Analytics](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Palabra clave RegEx

Hola de uso después de hello de sintaxis toouse **RegEx** palabra clave en una búsqueda de registros.  Puede usar Hola otras secciones de esta sintaxis de artículo toodetermine Hola de expresión regular de hello propio.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Por ejemplo, toouse una alerta de tooreturn de expresión regular se registra con un tipo de *advertencia* o *Error*, usaría Hola después de la búsqueda de registros.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Coincidencias parciales
Tenga en cuenta que expresión regular Hola debe coincidir con texto completo de hello de propiedad Hola.  Las coincidencias parciales no devolverán ningún registro.  Por ejemplo, si se tratara de registros tooreturn desde un equipo denominado srv01.contoso.com, Hola después de la búsqueda de registros sería **no** devolver todos los registros.

    Computer=RegEx("srv..")

Esto es porque solo Hola primera parte del nombre de hello coincide con la expresión regular de Hola.  Hello siguiente se buscan dos registros devolvería registros desde este equipo porque coinciden con la totalidad del nombre de Hola.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Caracteres
Especifique diferentes caracteres.

| Character | Descripción | Ejemplo | Coincidencias de ejemplo |
|:--|:--|:--|:--|
| a | Una aparición del carácter de Hola. | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| . | Cualquier carácter individual. | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Cero o una aparición del carácter de Hola. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Cero o más apariciones del carácter de Hola. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Una o más apariciones del carácter de Hola. | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Coincide con cualquier carácter individual entre corchetes Hola | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Coincide con un carácter individual en el intervalo de saludo.  Puede incluir varios intervalos. | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Ninguno de los caracteres de hello corchetes Hola | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Ninguno de los caracteres de hello en el intervalo de saludo. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Coincidencia con un intervalo de caracteres numéricos. | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | Cualquier cadena de caracteres. | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Varias repeticiones de carácter
Especifique varias repeticiones de un determinado carácter.

| Character | Descripción | Ejemplo | Coincidencias de ejemplo |
|:--|:--|:--|:--|
| a{n} |  *n*apariciones de caracteres de Hola. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*o más apariciones de caracteres de Hola. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*demasiado*m* apariciones del carácter de Hola. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Expresiones lógicas
Seleccione entre varios valores.

| Character | Descripción | Ejemplo | Coincidencias de ejemplo |
|:--|:--|:--|:--|
| &#124; | O lógico.  Devuelve el resultado si hay coincidencia en una de las expresiones. | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | Warning (Advertencia)<br>Error |
| & | Y lógico.  Devuelve el resultado si hay coincidencia en ambas expresiones. | EventData=regex("(Security.\*&.\*success.\*)") | Auditoría correcta de seguridad |


## <a name="literals"></a>Literales
Convertir caracteres tooliteral de caracteres especiales.  Esto incluye caracteres que proporcionan funcionalidad tooregular expresiones como?-\*^\[\]{}\(\)+\|. &.

| Character | Descripción | Ejemplo | Coincidencias de ejemplo |
|:--|:--|:--|:--|
| \\ | Convierte un literal de tooa de carácter especial. | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [Error]Archivo no encontrado.<br>Error-Archivo no encontrado. |


## <a name="next-steps"></a>Pasos siguientes

* Familiarizarse con [búsquedas de registro](log-analytics-log-searches.md) tooview y analizar los datos en el repositorio de análisis de registros de Hola.
