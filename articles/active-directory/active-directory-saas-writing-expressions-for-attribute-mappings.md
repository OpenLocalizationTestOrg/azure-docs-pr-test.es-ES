---
title: "aaaWriting expresiones para la asignación de atributo en Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los valores de atributo de tootransform de toouse expresión asignaciones en un formato aceptable durante el aprovisionamiento automatizado de objetos de aplicación de SaaS en Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Escritura de expresiones para la asignación de atributos en Azure Active Directory
Cuando se configura la aplicación de SaaS tooa aprovisionamiento, uno de los tipos de Hola de asignaciones de atributos que puede especificar es asignación con una expresión. Para ello, debe escribir los datos de usuario de una expresión de tipo de secuencia de comandos que le permite tootransform en formatos más aceptables para la aplicación de SaaS Hola.

## <a name="syntax-overview"></a>Información general sobre la sintaxis
sintaxis de Hola para las expresiones para asignaciones de atributos es recuerda a de Visual Basic para las funciones de aplicaciones (VBA).

* la expresión completa Hola debe definirse en términos de funciones, que constan de un nombre seguido de argumentos entre paréntesis: <br>
  *NombreDeFunción (&lt;&lt; argumento 1 &gt;&gt;, &lt;<argument N>&gt;)*
* Es posible anidar funciones dentro de otras. Por ejemplo: <br> *FunciónUno(FunciónDos(&lt;<argument1>&gt;))*
* Puede transformar tres tipos diferentes de argumentos en funciones:
  
  1. Atributos, que deben ir entre corchetes. Por ejemplo: [NombreAtributo]
  2. Constantes de cadena, que deben ir entre comillas. Por ejemplo: "Estados Unidos"
  3. Otras funciones. Por ejemplo: FunciónUna(<<argument1>>, FunciónDos(<<argument2>>))
* Para las constantes de cadena, si necesita una barra diagonal inversa (\) o comillas dobles (") en la cadena de hello, se deben convertirse con símbolo de barra diagonal inversa (\) Hola. Por ejemplo: "Company name: \"Contoso\""

## <a name="list-of-functions"></a>Lista de funciones
[Append](#append)&nbsp;&nbsp;&nbsp;&nbsp;[FormatDateTime](#formatdatetime)&nbsp;&nbsp;&nbsp;&nbsp;[Join](#join)&nbsp;&nbsp;&nbsp;&nbsp;[Mid](#mid)&nbsp;&nbsp;&nbsp;&nbsp;[Not](#not)&nbsp;&nbsp;&nbsp;&nbsp;[Sustituya](#replace)&nbsp;&nbsp;&nbsp;&nbsp;[StripSpaces](#stripspaces)&nbsp;&nbsp;&nbsp;&nbsp;[Switch](#switch)

- - -
### <a name="append"></a>Append
**Función:**<br> Append(source, suffix)

**Descripción**<br> Toma un valor de cadena de origen y lo anexa Hola sufijo toohello de sus extremos.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |Normalmente es el nombre del atributo de Hola Hola objeto de origen |
| **suffix** |Obligatorio |String |cadena de Hola que desea tooappend toohello final del valor de origen de Hola. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Función:**<br> FormatDateTime(source, inputFormat, outputFormat)

**Descripción:**<br> adopta una cadena de fecha en un formato y la convierte a un formato distinto.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |Normalmente es el nombre del atributo de Hola Hola objeto de origen. |
| **inputFormat** |Obligatorio |String |Formato esperado del valor de origen de Hola. Para conocer los formatos admitidos, consulte [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Obligatorio |String |Formato de fecha de salida de hello. |

- - -
### <a name="join"></a>Unión
**Función:**<br> Join(separator, source1, source2, …)

**Descripción**<br> Join() es tooAppend() similar, salvo que puede combinar varios **origen** valores de cadena en una sola cadena y cada valor estarán separado por una **separador** cadena.

Si uno de los valores del origen de hello es un atributo multivalor, cada valor de ese atributo será el valor del separador de hello combinadas juntos, separados.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **separator** |Obligatorio |String |Cadena usa valores de origen tooseparate cuando están concatenados en una sola cadena. Puede ser "" si no es necesario ningún separador. |
| **origen1  … origenN ** |Obligatorio, número variable de veces |String |Valores de cadena toobe unida entre sí. |

- - -
### <a name="mid"></a>Mid
**Función:**<br> Mid(source, start, length)

**Descripción**<br> Devuelve una subcadena del valor de origen de Hola. Una subcadena es una cadena que contiene solo algunos de los caracteres de Hola de cadena de origen de Hola.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |Normalmente es el nombre del atributo de Hola. |
| **start** |Obligatorio |integer |Índice de hello **origen** cadena donde debe comenzar la subcadena. Primer carácter de la cadena de hello tiene el índice de 1, el segundo carácter tiene el índice 2 y así sucesivamente. |
| **length** |Obligatorio |integer |Longitud de la subcadena de Hola. Si la longitud termina fuera hello **origen** cadena, función devuelve la subcadena de **iniciar** índice hasta el final de **origen** cadena. |

- - -
### <a name="not"></a>Not
**Función:**<br> Not(source)

**Descripción**<br> Voltea Hola valor booleano de hello **origen**. Si el valor de **source** es "*True*", devuelve "*False*". De lo contrario, devuelve "*True*".

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |Cadena booleana |Los valores de **source** esperados son "True" o "False". |

- - -
### <a name="replace"></a>Replace
**Función:**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**Descripción:**<br>
Reemplaza valores dentro de una cadena. Funciona de manera diferente dependiendo de los parámetros de hello proporciona:

* Cuando se proporcionan **oldValue** y **replacementValue**:
  
  * Reemplaza todas las apariciones de oldValue en origen Hola con un valor de reemplazo
* Cuando se proporcionan **oldValue** y **template**:
  
  * Reemplaza todas las apariciones de hello **oldValue** en hello **plantilla** con hello **origen** valor
* Cuando se proporcionan **oldValueRegexPattern**, **oldValueRegexGroupName** y **replacementValue**:
  
  * Reemplaza todos los valores que coinciden con Valoranteriormodeloderegeneración de cadena de origen de hello con un valor de reemplazo
* Cuando se proporcionan **oldValueRegexPattern**, **oldValueRegexGroupName** y **replacementPropertyName**:
  
  * Si **source** tiene algún valor, se devuelve **source**
  * Si **origen** no tiene ningún valor, se utiliza **Valoranteriormodeloderegeneración** y **Valoranteriornombregruporegeneración** tooextract el valor de reemplazo de propiedad Hola con  **Nombrepropiedadreemplazo**. Valor de reemplazo se devuelve como resultado de hello

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |Normalmente es el nombre del atributo de Hola Hola objeto de origen. |
| **oldValue** |Opcional |String |Valor toobe reemplazado en **origen** o **plantilla**. |
| **regexPattern** |Opcional |String |Patrón de expresión regular de Hola valor toobe reemplazado en **origen**. O bien, cuando se usa Nombrepropiedadreemplazo, tooextract valor de propiedad de reemplazo de modelo. |
| **regexGroupName** |Opcional |String |Nombre del grupo de hello dentro de **Modeloderegeneración**. Sólo cuando se utilice replacementPropertyName, extraeremos el valor de este grupo como replacementValue de la propiedad de reemplazo. |
| **replacementValue** |Opcional |String |Tooreplace nuevo de valor antiguo con. |
| **replacementAttributeName** |Opcional |String |Nombre de hello atributo toobe utilizado para el valor de reemplazo, cuando el origen no tiene ningún valor. |
| **template** |Opcional |String |Cuando **plantilla** se proporciona el valor, se buscará **oldValue** en Hola plantilla y reemplazarlo con el valor de origen. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Función:**<br> StripSpaces(source)

**Descripción**<br> Quita todo el espacio ("") caracteres de hello cadena de origen.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |**origen** tooupdate de valor. |

- - -
### <a name="switch"></a>Switch
**Función:**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**Descripción:**<br> Cuando el valor de **source** coincide con una **key**, devuelve el **value** de dicha **key**. Si el valor de **source** no coincide con ninguna clave, devuelve **defaultValue**.  Los parámetros **key** y **value** siempre deben estar emparejados. función Hello siempre espera un número par de parámetros.

**Parámetros:**<br> 

| Nombre | Obligatorio/Repetición | Tipo | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |String |**Origen** tooupdate de valor. |
| **defaultValue** |Opcional |String |Toobe de valor predeterminado utilizado cuando el origen no coincide con ninguna clave. Puede tratarse de una cadena vacía (""). |
| **key** |Obligatorio |String |**Clave** toocompare **origen** valor con. |
| **value** |Obligatorio |String |Valor de reemplazo para hello **origen** clave Hola coincidente. |

## <a name="examples"></a>Ejemplos
### <a name="strip-known-domain-name"></a>Seccionar un nombre de dominio conocido
Deberá toostrip un nombre de dominio tooobtain de correo electrónico de un usuario un nombre de usuario. <br>
Por ejemplo, si el dominio de hello es "contoso.com", podría utilizar Hola siguiente expresión:

**Expresión:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Ejemplo de entrada y salida:** <br>

* **ENTRADA** (mail): "john.doe@contoso.com"
* **SALIDA**: "john.doe"

### <a name="append-constant-suffix-toouser-name"></a>Anexar sufijo constante toouser nombre
Si usas un espacio aislado de Salesforce, tendrá que tooappend un tooall sufijos adicionales los nombres de usuario antes de sincronizarlos.

**Expresión:** <br>
`Append([userPrincipalName], ".test"))`

**Entrada/salida de ejemplo:** <br>

* **ENTRADA**: (userPrincipalName): "John.Doe@contoso.com"
* **ENTRADA**:  "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Generar el alias de usuario concatenando partes de nombre y apellidos
Deberá toogenerate un alias de usuario realizando primero 3 letras del nombre del usuario y las 5 primeras letras del apellido del usuario.

**Expresión:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Entrada/salida de ejemplo:** <br>

* **ENTRADA** (givenName): "John"
* **ENTRADA** (surname): "Doe"
* **SALIDA**: "JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Fecha de resultado como una cadena en un formato determinado
Desea que la aplicación de SaaS de tooa toosend fechas en un formato determinado. <br>
Por ejemplo, desea tooformat fechas para ServiceNow.

**Expresión:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Entrada/salida de ejemplo:**

* **ENTRADA** (extensionAttribute1): "20150123105347.1Z"
* **SALIDA**: "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Reemplazar un valor basado en un conjunto predefinido de opciones
Necesita la zona de horaria de hello toodefine del usuario de hello basado en código de estado de hello almacenada en Azure AD. <br>
Si el código de estado de hello no coincide con cualquiera de las opciones de hello predefinido, utilice el valor predeterminado de "Australia/Sydney".

**Expresión:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Entrada/salida de ejemplo:**

* **ENTRADA** (state): "QLD"
* **SALIDA**: "Australia/Brisbane"

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS](active-directory-saas-app-provisioning.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

