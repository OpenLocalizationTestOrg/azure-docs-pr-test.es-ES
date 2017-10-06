---
title: 'Azure AD Connect Sync: referencia de funciones | Microsoft Docs'
description: "Referencia de expresiones declarativas de aprovisionamiento en la sincronización de Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect Sync: referencia de funciones
En Azure AD Connect, las funciones son toomanipulate usa un valor de atributo durante la sincronización.  
Sintaxis de las funciones de Hola Hola se expresa mediante Hola siguiendo el formato:  
`<output type> FunctionName(<input type> <position name>, ..)`

Si una función está sobrecargada y acepta varias sintaxis, se enumeran todas las sintaxis válidas.  
Hola funciones están fuertemente tipadas y comprueban que coincide con el tipo de hello documentado pasado tipo hello.  
Si no coincide con el tipo de hello, se produce un error.

tipos de Hola se expresan con hello según la sintaxis:

* **bin** : binario
* **bool** : booleano
* **dt** : fecha y hora UTC
* **enum** : enumeración de constantes conocidas
* **EXP** : esperaba una expresión, que es tooevaluate tooa un valor booleano
* **mvbin** : binario de varios valores
* **mvstr** : cadena multivalor
* **mvref** : referencia multivalor
* **num** : numérico
* **ref** : referencia
* **str** : cadena
* **var** : una variante de (casi) cualquier otro tipo
* **void** : no devuelve un valor

Hola las funciones tienen tipos de hello **mvbin**, **mvstr**, y **mvref** sólo puede trabajar en atributos con varios valores. Las funciones con **bin**, **str** y **ref** funcionan en atributos con un solo valor y con varios valores.

## <a name="functions-reference"></a>Referencia de funciones
| Lista de funciones |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificate** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[ CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Conversión** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Fecha y hora** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Directorio** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Evaluación** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Matemáticas** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Con varios valores** | | | | |
| [Contains](#contains) |[Recuento](#count) |[Elemento](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[Dividir](#split) | | |
| **Flujo de programa** | | | | |
| [Error](#error) |[IIF](#iif) |[Select](#select) |[Switch](#switch) | |
| [Where](#where) |[With](#with) | | | |
| **Texto** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Sustituya](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Descripción**  
Hola función BitAnd establece los bits especificados en un valor.

**Sintaxis:**  
`num BitAnd(num value1, num value2)`

* value1, value2: valores numéricos que deberían estar unidos por el operador AND

**Comentarios:**  
Esta función convierte ambos representación binaria de parámetros toohello y establece un bit:

* 0 - si uno o ambos bits correspondientes de Hola *máscara* y *marca* son 0
* 1 - si ambos bits correspondientes de hello son 1.

En otras palabras, devuelve 0 en todos los casos excepto cuando los bits correspondientes de Hola de ambos parámetros son 1.

**Ejemplo:**  
`BitAnd(&HF, &HF7)`  
Devuelve 7 porque hexadecimal "F" y "F7" evaluación el valor de toothis.

- - -
### <a name="bitor"></a>BitOr
**Descripción**  
Hola función BitOr establece los bits especificados en un valor.

**Sintaxis:**  
`num BitOr(num value1, num value2)`

* value1, value2: valores numéricos que deberían estar unidos por el operador OR

**Comentarios:**  
Esta función convierte ambos representación binaria de parámetros toohello y establece un bit too1 si uno o ambos bits correspondientes de Hola de máscara y marca son 1 y too0 si ambos bits correspondientes de hello son 0. En otras palabras, devuelve 1 en todos los casos excepto cuando los bits correspondientes de Hola de ambos parámetros son 0.

- - -
### <a name="cbool"></a>CBool
**Descripción**  
Hola función CBool devuelve que un valor booleano en función de hello evaluar expresión

**Sintaxis:**  
`bool CBool(exp Expression)`

**Comentarios:**  
Si Hola se evalúa como tooa valor distinto de cero, CBool devuelve True, en caso contrario devuelve False.

**Ejemplo:**  
`CBool([attrib1] = [attrib2])`  

Devuelve True si ambos atributos tienen Hola el mismo valor.

- - -
### <a name="cdate"></a>CDate
**Descripción**  
Hola función CDate devuelve una fecha y hora UTC de una cadena. DateTime no es un tipo de atributo nativo en Sincronización pero lo usan algunas funciones.

**Sintaxis:**  
`dt CDate(str value)`

* Valor: una cadena con una fecha, hora y opcionalmente, una zona horaria

**Comentarios:**  
Hola devolvió una cadena siempre es en UTC.

**Ejemplo:**  
`CDate([employeeStartTime])`  
Devuelve una fecha y hora según el tiempo de inicio del empleado de Hola

`CDate("2013-01-10 4:00 PM -8")`  
Devuelve un valor DateTime que representa "2013-01-11 12:00 AM".








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Descripción**  
Devuelve Hola valores de Oid de todas las extensiones críticas Hola de un objeto de certificado.

**Sintaxis:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certformat"></a>CertFormat
**Descripción**  
Devuelve Hola nombre del formato de Hola de este certificado X.509v3.

**Sintaxis:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Descripción**  
Devuelve Hola alias asociado para un certificado.

**Sintaxis:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certhashstring"></a>CertHashString
**Descripción**  
Devuelve Hola valor hash SHA1 de certificados X.509v3 hello como una cadena hexadecimal.

**Sintaxis:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certissuer"></a>CertIssuer
**Descripción**  
Devuelve Hola nombre de entidad emisora de certificados de Hola que emitió el certificado X.509v3 de Hola.

**Sintaxis:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Descripción**  
Devuelve Hola nombre distintivo del emisor de certificado de Hola.

**Sintaxis:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Descripción**  
Devuelve Hola Oid del emisor de certificado de Hola.

**Sintaxis:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Descripción**  
Devuelve información de algoritmo de clave de Hola de este certificado X.509v3 como una cadena.

**Sintaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Descripción**  
Devuelve los parámetros de algoritmo de clave de hello certificado X.509v3 de hello como una cadena hexadecimal.

**Sintaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Descripción**  
Devuelve emisor y el asunto de hello nombres de un certificado.

**Sintaxis:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.
*   X509NameType: Hola valor X509NameType asunto Hola.
*   includesIssuerName: nombre de emisor de hello tooinclude true; en caso contrario, false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Descripción**  
Devuelve la fecha de hello en hora local después del cual un certificado ya no es válido.

**Sintaxis:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Descripción**  
Devuelve la fecha de hello en hora local en el que un certificado es válido.

**Sintaxis:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Descripción**  
Devuelve Hola Oid de clave pública de hello certificado X.509v3 de Hola.

**Sintaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Descripción**  
Devuelve Hola Oid de parámetros de clave pública de hello certificado X.509v3 de Hola.

**Sintaxis:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Descripción**  
Devuelve el número de serie de Hola de certificado X.509v3 de Hola.

**Sintaxis:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Descripción**  
Hola devuelve Oid del algoritmo de hello utiliza firma de hello toocreate de un certificado.

**Sintaxis:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certsubject"></a>CertSubject
**Descripción**  
Obtiene Hola nombre distintivo del sujeto de un certificado.

**Sintaxis:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Descripción**  
Devuelve Hola nombre distintivo del sujeto de un certificado.

**Sintaxis:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Descripción**  
Devuelve Hola Oid del nombre de sujeto de Hola de un certificado.

**Sintaxis:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**Descripción**  
Devuelve Hola huella digital de un certificado.

**Sintaxis:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="certversion"></a>CertVersion
**Descripción**  
Devuelve Hola versión en formato de un certificado X.509.

**Sintaxis:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.

- - -
### <a name="cguid"></a>CGuid
**Descripción**  
Hola función CGuid convierte la representación de cadena de Hola de una representación binaria de tooits GUID.

**Sintaxis:**  
`bin CGuid(str GUID)`

* Una cadena con un formato que sigue este patrón: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**Descripción**  
función de Hello Contains busca una cadena dentro de un atributo multivalor

**Sintaxis:**  
`num Contains (mvstring attribute, str search)` - distingue mayúsculas y minúsculas  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - distingue mayúsculas y minúsculas

* atributo: Hola atributo multivalor toosearch.
* búsqueda: cadena toofind en atributo Hola.
* Casetype: CaseInsensitive o CaseSensitive.

Devuelve el índice de atributo multivalor Hola donde se encontró la cadena de Hola. se devuelve 0 si no se encuentra la cadena de Hola.

**Comentarios:**  
Para los atributos de cadena multivalor, Hola encontrar subcadenas en valores de hello.  
Para los atributos de referencia, hello cadena buscada debe coincidir exactamente con hello valor toobe considera a una coincidencia.

**Ejemplo:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Si el atributo proxyAddresses de hello tiene una dirección de correo electrónico principal (indicada por las mayúsculas "SMTP:"), a continuación, devolver el atributo proxyAddress de hello, devolver un error en caso contrario.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Descripción**  
Hola ConvertFromBase64 función convierte Hola especifica cadena base64 del valor tooa regular.

**Sintaxis:**  
`str ConvertFromBase64(str source)` da por hecho que se usará Unicode para la codificación.  
`str ConvertFromBase64(str source, enum Encoding)`

* source: cadena codificada en Base64  
* Codificación: Unicode, ASCII, UTF8

**Ejemplo**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Ambos ejemplos devuelven "*Hola a todos*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Descripción**  
Hola ConvertFromUTF8Hex función convierte Hola especifica la cadena de tooa valor codificado en hexadecimal UTF8.

**Sintaxis:**  
`str ConvertFromUTF8Hex(str source)`

* origen: cadena codificada de 2 bytes UTF8

**Comentarios:**  
Hola diferencia entre esta función y ConvertFromBase64([],UTF8) que dan lugar a hello es descriptivo para el atributo DN de Hola.  
Azure Active Directory utiliza este formato como DN.

**Ejemplo:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
devuelve "*Hello world!*".

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Descripción**  
Hola función ConvertToBase64 convierte una cadena base64 de Unicode tooa de cadena.  
Convierte el valor de Hola de una matriz de representación de cadena equivalente de tooits de enteros que se codifica con dígitos de base 64.

**Sintaxis:**  
`str ConvertToBase64(str source)`

**Ejemplo:**  
`ConvertToBase64("Hello world!")`  
devuelve "SABlAGwAbABvACAAdwBvAHIAbABkACEA".

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Descripción**  
Hola función ConvertToUTF8Hex convierte un valor codificado en hexadecimal UTF8 tooa de cadena.

**Sintaxis:**  
`str ConvertToUTF8Hex(str source)`

**Comentarios:**  
formato de salida de Hello de esta función se utiliza por Azure Active Directory como formato del atributo DN.

**Ejemplo:**  
`ConvertToUTF8Hex("Hello world!")`  
devuelve 48656C6C6F20776F726C6421.

- - -
### <a name="count"></a>Recuento
**Descripción**  
Hola función Count devuelve el número de Hola de elementos de un atributo multivalor

**Sintaxis:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Descripción**  
Hola función CNum toma una cadena y devuelve un tipo de datos numéricos.

**Sintaxis:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Descripción**  
Convierte un atributo de referencia de cadena tooa

**Sintaxis:**  
`ref CRef(str value)`

**Ejemplo:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Descripción**  
Hello para la función CStr Convierte el tipo de datos de cadena de tooa.

**Sintaxis:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* value: puede ser un valor numérico, un atributo de referencia o un valor booleano.

**Ejemplo:**  
`CStr([dn])`  
podría devolver "cn=Joe,dc=contoso,dc=com"

- - -
### <a name="dateadd"></a>DateAdd
**Descripción**  
Devuelve una fecha que contiene un toowhich de fecha que se ha agregado un intervalo de tiempo especificado.

**Sintaxis:**  
`dt DateAdd(str interval, num value, dt date)`

* intervalo: expresión de cadena que es el intervalo de saludo de tiempo que desea tooadd. cadena de Hello debe tener uno de hello siguientes valores:
  * yyyy Año
  * q Trimestre
  * m Mes
  * y Día del año
  * d Día
  * w Día de la semana
  * ww Semana
  * h Hora
  * n Minuto
  * s Segundo
* valor: Hola número de unidades que desea tooadd. Puede ser positivo (tooget fechas en hello futuras) o negativo (tooget fechas en hello anterior).
* fecha: fecha y hora se agrega el intervalo de saludo de toowhich de fecha que representa.

**Ejemplo:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
agrega 3 meses y devuelve un valor DateTime que representa "2001-04-01".

- - -
### <a name="datefromnum"></a>DateFromNum
**Descripción**  
Hola función DateFromNum convierte el valor de tooa de formato de fecha de AD tipo DateTime.

**Sintaxis:**  
`dt DateFromNum(num value)`

**Ejemplo:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
devuelve un valor DateTime que representa 2012-01-01 23:00:00.

- - -
### <a name="dncomponent"></a>DNComponent
**Descripción**  
Hola función DNComponent devuelve el valor Hola de un componente DN especificado desde la izquierda.

**Sintaxis:**  
`str DNComponent(ref dn, num ComponentNumber)`

* DN: Hola referencia atributo toointerpret
* ComponentNumber: componente hello en hello DN tooreturn

**Ejemplo:**  
`DNComponent([dn],1)`  
si dn es "cn=Joe,ou=…", devuelve Joe.

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Descripción**  
Hola función DNComponentRev devuelve valor Hola de un componente DN especificado desde la derecha (Hola final).

**Sintaxis:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* DN: Hola referencia atributo toointerpret
* ComponentNumber - componente hello en hello DN tooreturn
* Opciones: DC, ignora todos los componentes con “dc=”

**Ejemplo:**  
Si dn es "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
Ambos devuelven US.

- - -
### <a name="error"></a>Error
**Descripción**  
Hola función de Error es tooreturn usado un error personalizado.

**Sintaxis:**  
`void Error(str ErrorMessage)`

**Ejemplo:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Si Hola atributo accountName no está presente, produce un error en el objeto de Hola.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Descripción**  
Hola función EscapeDNComponent toma un componente de un DN y secuencias de escape, por lo que puede representarse en LDAP.

**Sintaxis:**  
`str EscapeDNComponent(str value)`

**Ejemplo:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Se asegura de objeto Hola puede crearse en un directorio LDAP, incluso si el atributo de hello displayName tiene caracteres que deben tener escape en LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Descripción**  
función FormatDateTime de Hello es tooformat usa una cadena de fecha y hora tooa con un formato especificado

**Sintaxis:**  
`str FormatDateTime(dt value, str format)`

* valor: un valor en formato de fecha y hora de Hola
* formato: una cadena que representa Hola formato tooconvert a.

**Comentarios:**  
Hola valores posibles para el formato de hello puede encontrarse aquí: [formatos de fecha y hora definidos por el usuario (función Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Ejemplo:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
Genera "2007-12-25".

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
Puede generar "20140905081453.0Z".

- - -
### <a name="guid"></a>GUID
**Descripción**  
Hola función GUID genera un nuevo GUID aleatorio

**Sintaxis:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Descripción**  
Hola función IIF devuelve uno de un conjunto de valores posibles basado en una condición especificada.

**Sintaxis:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* condición: cualquier valor o expresión que se puede evaluar tootrue o false.
* ValorSiVerdadero: si la condición de Hola se evalúa como tootrue, Hola devolvió el valor.
* valorSiFalse: si la condición de Hola se evalúa como toofalse, Hola devolvió el valor.

**Ejemplo:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Si el usuario de hello es una persona en prácticas, devuelve Hola alias de un usuario con "t-" agregados toohello a partir de ella, else devuelve los alias del usuario de hello tal cual.

- - -
### <a name="instr"></a>InStr
**Descripción**  
Hola función InStr busca Hola primera aparición de una subcadena en una cadena

**Sintaxis:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* comprobarcadena: cadena toobe buscada
* coincidircadena: cadena toobe encuentra
* inicio: iniciar posición toofind Hola subcadena
* compare: vbTextCompare o vbBinaryCompare

**Comentarios:**  
Posición de hello devuelve donde se encontró la subcadena de Hola o 0 si no encuentra.

**Ejemplo:**  
`InStr("hello quick brown fox","quick")`  
Evalues too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Se evalúa como too7

- - -
### <a name="instrrev"></a>InStrRev
**Descripción**  
Hola función InStrRev busca la última aparición de una subcadena de hello en una cadena

**Sintaxis:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* comprobarcadena: cadena toobe buscada
* coincidircadena: cadena toobe encuentra
* inicio: iniciar posición toofind Hola subcadena
* compare: vbTextCompare o vbBinaryCompare

**Comentarios:**  
Posición de hello devuelve donde se encontró la subcadena de Hola o 0 si no encuentra.

**Ejemplo:**  
`InStrRev("abbcdbbbef","bb")`  
devuelve 7.

- - -
### <a name="isbitset"></a>IsBitSet
**Descripción**  
función Hello IsBitSet pruebas si un bit está establecido o no

**Sintaxis:**  
`bool IsBitSet(num value, num flag)`

* valor: un valor numérico que es evalúa. Flag: un valor numérico que tiene Hola bit toobe evaluada

**Ejemplo:**  
`IsBitSet(&HF,4)`  
Devuelve el valor True porque bit "4" está establecido en el valor hexadecimal de Hola "F"

- - -
### <a name="isdate"></a>IsDate
**Descripción**  
Si expresión Hola puede ser evalúa como un tipo de fecha y hora, Hola función IsDate evalúa tooTrue.

**Sintaxis:**  
`bool IsDate(var Expression)`

**Comentarios:**  
Usar toodetermine si CDate() pueda realizarse correctamente.

- - -
### <a name="iscert"></a>IsCert
**Descripción**  
Devuelve true si se pueden serializar los datos sin procesar de hello en el objeto de certificado X509Certificate2. NET.

**Sintaxis:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representación de matriz de bytes de un certificado X.509. matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.
- - -
### <a name="isempty"></a>IsEmpty
**Descripción**  
Si el atributo de hello está presente en hello CS o MV pero da como resultado una cadena vacía tooan, IsEmpty (función) Hola evalúa tooTrue.

**Sintaxis:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Descripción**  
Si la cadena de hello podría ser convertido tooa GUID, función isguid da como resultado de hello evalúa tootrue.

**Sintaxis:**  
`bool IsGuid(str GUID)`

**Comentarios:**  
un GUID se define como una cadena que sigue uno de estos patrones: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.

Usar toodetermine si CGuid() pueda realizarse correctamente.

**Ejemplo:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Si hello StrAttribute tiene un formato GUID, devuelve una representación binaria, en caso contrario, devuelven un valor Null.

- - -
### <a name="isnull"></a>IsNull
**Descripción**  
Si expresión Hola se evalúa como tooNull, función de hello IsNull devuelve true.

**Sintaxis:**  
`bool IsNull(var Expression)`

**Comentarios:**  
Para un atributo, un valor Null se expresa por falta de hello del atributo Hola.

**Ejemplo:**  
`IsNull([displayName])`  
Devuelve True si el atributo de hello no está presente en hello CS o MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Descripción**  
Si la expresión de hello es null o una cadena vacía, función de hello IsNullOrEmpty devuelve true.

**Sintaxis:**  
`bool IsNullOrEmpty(var Expression)`

**Comentarios:**  
Para un atributo, da como resultado tooTrue si el atributo de hello no está presente o está presente pero es una cadena vacía.  
inverso de Hola de esta función se denomina IsPresent.

**Ejemplo:**  
`IsNullOrEmpty([displayName])`  
Devuelve True si el atributo de hello no está presente o es una cadena vacía en hello CS o MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Descripción**  
Hola función IsNumeric devuelve un valor booleano que indica si una expresión se puede evaluar como un tipo de número.

**Sintaxis:**  
`bool IsNumeric(var Expression)`

**Comentarios:**  
Usar toodetermine si CNum() puede ser una expresión de hello tooparse correcta.

- - -
### <a name="isstring"></a>IsString
**Descripción**  
Si la expresión de hello puede se evaluado tooa tipo string, función isstring da de hello evalúa tooTrue.

**Sintaxis:**  
`bool IsString(var expression)`

**Comentarios:**  
Usar toodetermine si CStr() puede ser una expresión de hello tooparse correcta.

- - -
### <a name="ispresent"></a>IsPresent
**Descripción**  
Si expresión Hola se evalúa como cadena tooa que no es Null y no está vacío, a continuación, Hola IsPresent función devuelve true.

**Sintaxis:**  
`bool IsPresent(var expression)`

**Comentarios:**  
inverso de Hola de esta función se denomina IsNullOrEmpty.

**Ejemplo:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Elemento
**Descripción**  
Hola función Item devuelve un elemento de un cadena o atributo multivalor.

**Sintaxis:**  
`var Item(mvstr attribute, num index)`

* attribute: atributo de varios valores
* índice: elemento de tooan de índice de cadena multivalor Hola.

**Comentarios:**  
Hola función Item es útil junto con hello función Contains, ya que esta última función de hello devuelve el elemento de tooan de índice de Hola de atributo con varios valores de hello.

Se produce un error si el índice está fuera de los límites.

**Ejemplo:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Devuelve Hola dirección de correo electrónico principal.

- - -
### <a name="itemornull"></a>ItemOrNull
**Descripción**  
Hola función ItemOrNull devuelve un elemento de un cadena o atributo multivalor.

**Sintaxis:**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute: atributo de varios valores
* índice: elemento de tooan de índice de cadena multivalor Hola.

**Comentarios:**  
Hola función ItemOrNull es útil junto con hello función Contains, ya que esta última función de hello devuelve el elemento de tooan de índice de Hola de atributo con varios valores de hello.

Si el índice está fuera de los límites, devuelve un valor Null.

- - -
### <a name="join"></a>Join
**Descripción**  
función de combinación de Hello toma una cadena multivalor y devuelve una cadena de un solo valor con el separador especificado insertado entre cada elemento.

**Sintaxis:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* atributo: atributo multivalor que contiene cadenas toobe unido.
* delimitador: cualquier cadena, tooseparate usado Hola subcadenas en hello devuelve la cadena. Si se omite, Hola carácter de espacio ("") se utiliza. Si Delimiter es una cadena de longitud cero ("") o Nothing, todos los elementos de lista de Hola se concatenan sin delimitadores.

**Comentarios**  
Hay paridad entre las funciones de división y combinación de Hola. Hola función Join toma una matriz de cadenas y une mediante una cadena de delimitador, tooreturn una sola cadena. Hola función Split toma una cadena y la separa en delimitador de hello, tooreturn una matriz de cadenas. Sin embargo, una diferencia clave es que Join puede concatenar cadenas con cualquier cadena de delimitación, mientras que attribute puede separar solo cadenas mediante un delimitador de carácter único.

**Ejemplo:**  
`Join([proxyAddresses],",")`  
Podría devolver: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Descripción**  
Hola función LCase convierte todos los caracteres en un caso de toolower de cadena.

**Sintaxis:**  
`str LCase(str value)`

**Ejemplo:**  
`LCase("TeSt")`  
devuelve "test".

- - -
### <a name="left"></a>Left
**Descripción**  
función Left Hola devuelve un número especificado de caracteres desde la izquierda de Hola de una cadena.

**Sintaxis:**  
`str Left(str string, num NumChars)`

* cadena: Hola tooreturn caracteres de una cadena de
* NumChars: un número que identifica el número de Hola de tooreturn de caracteres desde el principio de hello (izquierda) de cadena

**Comentarios:**  
Una cadena que contiene los primeros caracteres numChars hello en cadena:

* Con numChars = 0, se devuelve una cadena vacía.
* Con numChars < 0, se devuelve una cadena de entrada.
* Si la cadena es null, se devuelve una cadena vacía.

Si la cadena contiene menos caracteres que el número de hello especificado en numChars, se devuelve un toostring idénticos de cadena (que es, que contiene todos los caracteres en el parámetro 1).

**Ejemplo:**  
`Left("John Doe", 3)`  
devuelve “Joh”.

- - -
### <a name="len"></a>Len
**Descripción**  
Hola función Len devuelve el número de caracteres en una cadena.

**Sintaxis:**  
`num Len(str value)`

**Ejemplo:**  
`Len("John Doe")`  
devuelve 8.

- - -
### <a name="ltrim"></a>LTrim
**Descripción**  
Hola función LTrim quita los espacios en blanco de una cadena.

**Sintaxis:**  
`str LTrim(str value)`

**Ejemplo:**  
`LTrim(" Test ")`  
devuelve "Test".

- - -
### <a name="mid"></a>Mid
**Descripción**  
Hola Mid función devuelve un número especificado de caracteres desde la posición especificada en una cadena.

**Sintaxis:**  
`str Mid(str string, num start, num NumChars)`

* cadena: Hola tooreturn caracteres de una cadena de
* iniciar: un número que identifica Hola a partir de la posición en la cadena de caracteres de tooreturn de
* NumChars: un número que identifica el número de Hola de tooreturn de caracteres desde la posición en la cadena

**Comentarios:**  
devuelve caracteres numChars que comienzan por la posición de inicio en una cadena.  
Una cadena que contiene caracteres numChars de la posición de inicio en una cadena:

* Con numChars = 0, se devuelve una cadena vacía.
* Con numChars < 0, se devuelve una cadena de entrada.
* Si iniciar > Hola longitud de cadena, devuelven la cadena de entrada.
* Con start <= 0, se devuelve la cadena de entrada.
* Si la cadena es null, se devuelve una cadena vacía.

Si no hay caracteres numChar restantes en la cadena de la posición de inicio, se devuelve el máximo de caracteres posible.

**Ejemplo:**  
`Mid("John Doe", 3, 5)`  
devuelve “hn Do”.

`Mid("John Doe", 6, 999)`  
Devuelve "Doe".

- - -
### <a name="now"></a>Now
**Descripción**  
Hello ahora función devuelve una fecha y hora especificar Hola fecha y hora, actual según tooyour fecha del sistema del equipo y la hora.

**Sintaxis:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Descripción**  
Hola función NumFromDate devuelve una fecha en formato de fecha de AD.

**Sintaxis:**  
`num NumFromDate(dt value)`

**Ejemplo:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
devuelve 129699324000000000.

- - -
### <a name="padleft"></a>PadLeft
**Descripción**  
función de Hello PadLeft rellena hacia la izquierda un tooa de cadena especificado longitud mediante el carácter de relleno proporcionado.

**Sintaxis:**  
`str PadLeft(str string, num length, str padCharacter)`

* cadena: Hola toopad de cadena.
* longitud: un entero que representa Hola deseado longitud de cadena.
* padCharacter: una cadena que consta de un toouse único carácter como carácter de relleno de Hola

**Comentarios:**

* Si la longitud de Hola de cadena es menor que la longitud, padCharacter es toohello repetidamente anexados principio (izquierda) de cadena hasta que tenga un toolength de igual longitud.
* PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.
* Si la longitud de Hola de cadena es mayor que la longitud de tooor igual, la cadena se devuelve sin cambios.
* Si la cadena tiene una longitud mayor que o igual toolength, se devuelve un toostring idénticos de cadena.
* Si la longitud de Hola de cadena es menor que la longitud, una nueva cadena de hello deseado se devuelve la longitud que contiene una cadena rellenada con un padCharacter.
* Si la cadena es null, la función hello devuelve una cadena vacía.

**Ejemplo:**  
`PadLeft("User", 10, "0")`  
devuelve "000000User".

- - -
### <a name="padright"></a>PadRight
**Descripción**  
función de Hello PadRight rellena hacia la derecha un tooa de cadena especificado longitud mediante el carácter de relleno proporcionado.

**Sintaxis:**  
`str PadRight(str string, num length, str padCharacter)`

* cadena: Hola toopad de cadena.
* longitud: un entero que representa Hola deseado longitud de cadena.
* padCharacter: una cadena que consta de un toouse único carácter como carácter de relleno de Hola

**Comentarios:**

* Si la longitud de Hola de cadena es menor que la longitud, padCharacter es toohello repetidamente anexados final (derecha) de cadena, hasta que tenga un toolength de igual longitud.
* PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.
* Si la longitud de Hola de cadena es mayor que la longitud de tooor igual, la cadena se devuelve sin cambios.
* Si la cadena tiene una longitud mayor que o igual toolength, se devuelve un toostring idénticos de cadena.
* Si la longitud de Hola de cadena es menor que la longitud, una nueva cadena de hello deseado se devuelve la longitud que contiene una cadena rellenada con un padCharacter.
* Si la cadena es null, la función hello devuelve una cadena vacía.

**Ejemplo:**  
`PadRight("User", 10, "0")`  
devuelve "User000000".

- - -
### <a name="pcase"></a>PCase
**Descripción**  
Hola función PCase convierte el primer carácter de cada palabra delimitada por espacios en el caso de tooupper de cadena de Hola y todos los demás caracteres se convierten toolower caso.

**Sintaxis:**  
`String PCase(string)`

**Comentarios:**

* Esta función no proporciona actualmente tooconvert grafía apropiada una palabra que esté completamente en mayúscula, por ejemplo, un acrónimo.

**Ejemplo:**  
`PCase("TEsT")`  
devuelve "test".

`PCase(LCase("TEST"))`  
devuelve "Test".

- - -
### <a name="randomnum"></a>RandomNum
**Descripción**  
Hola función RandomNum devuelve un número aleatorio entre un intervalo especificado.

**Sintaxis:**  
`num RandomNum(num start, num end)`

* iniciar: un número identificación Hola límite inferior de hello valor aleatorio toogenerate
* extremo: un número identificación Hola límite superior de hello valor aleatorio toogenerate

**Ejemplo:**  
`Random(100,999)`  
puede devolver 734.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Descripción**  
Hola función RemoveDuplicates toma una cadena multivalor y asegúrese de que cada valor sea único.

**Sintaxis:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Ejemplo:**  
`RemoveDuplicates([proxyAddresses])`  
devuelve un atributo proxyAddress saneado donde se han quitado todos los valores duplicados.

- - -
### <a name="replace"></a>Sustituya
**Descripción**  
Hola función Replace reemplaza todas las apariciones de una cadena de tooanother de cadena.

**Sintaxis:**  
`str Replace(str string, str OldValue, str NewValue)`

* cadena: una cadena tooreplace valores en.
* OldValue: Hola cadena toosearch para y tooreplace.
* NewValue: Hola tooreplace de cadena a.

**Comentarios:**  
función Hello reconoce Hola después monikers especiales:

* \n: nueva línea
* \r: retorno de carro
* \t: tabulación

**Ejemplo:**  
`Replace([address],"\r\n",", ")`  
Reemplaza CRLF por una coma y un espacio y podría provocar demasiado "One Microsoft Way, Redmond, WA, EE"

- - -
### <a name="replacechars"></a>ReplaceChars
**Descripción**  
Hola función ReplaceChars reemplaza todas las apariciones de caracteres que se encuentran en hello cadena ReplacePattern.

**Sintaxis:**  
`str ReplaceChars(str string, str ReplacePattern)`

* cadena: caracteres de una cadena tooreplace de.
* ReplacePattern: una cadena que contiene un diccionario con caracteres tooreplace.

formato de Hello es {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} que el origen es Hola carácter toofind y destino Hola cadena tooreplace con.

**Comentarios:**

* función Hello toma cada aparición de los orígenes definidos y los reemplaza con destinos de Hola.
* origen de Hello debe ser exactamente un carácter (unicode).
* origen de Hello no puede estar vacío ni ser más de un carácter (error de análisis).
* destino de Hello puede tener varios caracteres, por ejemplo ö:oe, β.
* destino de Hello puede estar vacía que indica que se deben quitar los caracteres de Hola.
* origen de Hello distingue mayúsculas de minúsculas y debe ser una coincidencia exacta.
* Hola, (coma) y: (dos puntos) son caracteres reservados y no se puede reemplazar utilizando esta función.
* Se omiten los espacios y otros caracteres en blanco en hello cadena ReplacePattern.

**Ejemplo:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Devuelve Raksmorgas.

`ReplaceChars("O’Neil",%ReplaceString%)`  
Devuelve "oneil", ya único TIC de hello es toobe definido quitado.

- - -
### <a name="right"></a>Right
**Descripción**  
función Right Hola devuelve un número especificado de caracteres de hello derecho (final) de una cadena.

**Sintaxis:**  
`str Right(str string, num NumChars)`

* cadena: Hola tooreturn caracteres de una cadena de
* NumChars: un número que identifica el número de Hola de tooreturn de caracteres de fin de hello (derecha) de cadena

**Comentarios:**  
Se devuelven caracteres NumChars desde la última posición de Hola de cadena.

Una cadena que contiene los últimos caracteres numChars hello en cadena:

* Con numChars = 0, se devuelve una cadena vacía.
* Con numChars < 0, se devuelve una cadena de entrada.
* Si la cadena es null, se devuelve una cadena vacía.

Si la cadena contiene menos caracteres que Hola número especificado en NumChars, se devuelve un toostring idénticos de cadena.

**Ejemplo:**  
`Right("John Doe", 3)`  
devuelve "Doe".

- - -
### <a name="rtrim"></a>RTrim
**Descripción**  
Hola función RTrim quita los espacios en blanco de una cadena.

**Sintaxis:**  
`str RTrim(str value)`

**Ejemplo:**  
`RTrim(" Test ")`  
devuelve "Test".

- - -
### <a name="select"></a>Seleccionar
**Descripción:**  
Procesa todos los valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.

**Sintaxis:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* elemento: representa un elemento atributo multivalor Hola
* atributo: atributo multivalor Hola
* expression: una expresión que devuelve una colección de valores
* condición: cualquier función que puede procesar un elemento atributo Hola

**Ejemplos:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Devolver todos los valores de hello Hola atributo multivalor OtroTeléfono una vez que se han quitado los guiones (-).

- - -
### <a name="split"></a>Dividir
**Descripción**  
Hola función Split toma una cadena separada por un delimitador y hace que una cadena multivalor.

**Sintaxis:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* valor: Hola cadena con un tooseparate de carácter delimitador.
* delimitador: único toobe de caracteres que se usa como delimitador de Hola.
* limit: número máximo de valores que se pueden devolver.

**Ejemplo:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Devuelve una cadena multivalor con 2 elementos útiles para el atributo proxyAddress de Hola.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Descripción**  
Hola función StringFromGuid toma un GUID binario y lo convierte en la cadena de tooa

**Sintaxis:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Descripción**  
Hola función StringFromSid convierte una matriz de bytes que contiene una cadena de tooa del identificador de seguridad.

**Sintaxis:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Descripción**  
función de conmutador de Hello es tooreturn usa un valor único basado en condiciones evaluadas.

**Sintaxis:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr: expresión Variant que desee tooevaluate.
* valor: toobe de valor devuelto si la expresión correspondiente de hello es True.

**Comentarios:**  
Hola argumento de la función de conmutador lista está formada por pares de expresiones y valores. Hola las expresiones se evalúan de izquierda tooright y se devuelve el valor de hello asociada Hola primera expresión tooevaluate tooTrue. Si las partes de hello no están correctamente emparejadas, se produce un error en tiempo de ejecución.

Por ejemplo, si expr1 es True, Switch devuelve value1. Si expr-1 es False, pero expr-2 es True, Switch devuelve value-2, etc.

Switch devuelve Nothing si:

* Ninguna de las expresiones de hello son True.
* la primera expresión es True de Hello tiene un valor correspondiente que es Null.

Switch evalúa todas las expresiones, aunque devuelva solo una de ellas. Por este motivo, debe vigilar efectos secundarios no deseados. Por ejemplo, si la evaluación de Hola de cualquier expresión tiene como resultado una división por cero error, se produce un error.

Valor también puede ser la función de Error de hello, lo que devolvería una cadena personalizada.

**Ejemplo:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Devuelve el idioma de hello hablado en algunas ciudades importantes, en caso contrario, devuelve un Error.

- - -
### <a name="trim"></a>Trim
**Descripción**  
función Trim Hello quita iniciales y finales de espacios en blanco de una cadena.

**Sintaxis:**  
`str Trim(str value)`  

**Ejemplo:**  
`Trim(" Test ")`  
devuelve "test".

`Trim([proxyAddresses])`  
Quita espacios para cada valor de atributo proxyAddress de hello iniciales y finales.

- - -
### <a name="ucase"></a>UCase
**Descripción**  
Hola función UCase convierte todos los caracteres en un caso de tooupper de cadena.

**Sintaxis:**  
`str UCase(str string)`

**Ejemplo:**  
`UCase("TeSt")`  
devuelve "test".

- - -
### <a name="where"></a>Where

**Descripción:**  
Devuelve un subconjunto de valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.

**Sintaxis:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* elemento: representa un elemento atributo multivalor Hola
* atributo: atributo multivalor Hola
* condición: cualquier expresión que se puede evaluar tootrue o false
* expression: una expresión que devuelve una colección de valores

**Ejemplo:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Devolver valores de certificado de hello en hello userCertificate de atributo con varios valores que no se ha caducado.

- - -
### <a name="with"></a>With
**Descripción**  
Hola con función proporciona un toosimplify de forma una expresión compleja mediante el uso de una variable toorepresent una subexpresión que aparece una o varias veces en la expresión compleja Hola.

**Sintaxis:**
`With(var variable, exp subExpression, exp complexExpression)`  
* variable: representa Hola subexpresión.
* subExpression: la que la variable representa.
* complexExpression: una expresión compleja.

**Ejemplo:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Es funcionalmente equivalente a:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Que devuelve solo los valores de los certificados vigentes en el atributo userCertificate de Hola.


- - -
### <a name="word"></a>Word
**Descripción**  
Hola función Word devuelve una palabra contenida dentro de una cadena según los parámetros que describen toouse de delimitadores de Hola y Hola word número tooreturn.

**Sintaxis:**  
`str Word(str string, num WordNumber, str delimiters)`

* cadena: Hola tooreturn de cadena de una palabra.
* WordNumber: un número que identifica qué número de palabras debe devolver.
* delimitadores: una cadena que representa los delimitadores de Hola que deben ser utilizados tooidentify palabras

**Comentarios:**  
Cada cadena de caracteres de cadena separados por hello uno de los caracteres de hello en los delimitadores se identifican como palabras:

* Si el número es < 1, se devuelve una cadena vacía.
* Si la cadena es Null, se devuelve una cadena vacía.

Si la cadena contiene menos palabras o si la cadena no contiene palabras identificadas por los delimitadores, se devuelve una cadena vacía.

**Ejemplo:**  
`Word("hello quick brown fox",3," ")`  
devuelve "brown".

`Word("This,string!has&many separators",3,",!&#")`  
devolvería "has".

## <a name="additional-resources"></a>Recursos adicionales
* [Explicación de las expresiones declarativas de aprovisionamiento](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Sincronización de Azure AD Connect: personalización de las opciones de sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
