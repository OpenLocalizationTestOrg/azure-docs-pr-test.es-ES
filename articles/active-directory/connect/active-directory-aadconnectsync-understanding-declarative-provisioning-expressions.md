---
title: 'Azure AD Connect: expresiones de aprovisionamiento declarativo | Microsoft Docs'
description: Explica las expresiones de aprovisionamiento declarativo Hola.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Sincronización de Azure AD Connect: conocimiento de expresiones de aprovisionamiento declarativo
La sincronización de Azure AD Connect se basa en el aprovisionamiento declarativo, que se introdujo en Forefront Identity Manager 2010. Le permite tooimplement la lógica de negocios de integración de identidad completa sin Hola necesidad toowrite el código compilado.

Una parte esencial del aprovisionamiento declarativo es el lenguaje de expresiones de hello utilizado en flujos de atributo. Hola idioma es un subconjunto de Microsoft® Visual Basic para aplicaciones (VBA). Este lenguaje se usa en Microsoft Office, y los usuarios con experiencia en VBScript también lo reconocerán. Hola lenguaje de expresiones de aprovisionamiento declarativo solo usa funciones y no es un lenguaje estructurado. No hay métodos ni instrucciones. En su lugar se anidan funciones tooexpress flujo de programa.

Para obtener más información, consulte [Bienvenido toohello Visual Basic para hacer referencia de lenguaje de las aplicaciones de Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).

atributos de Hello tienen establecimiento inflexible de tipos. Una función solo acepta atributos del tipo correcto de Hola. También distinguen mayúsculas de minúsculas. Es preciso usar correctamente las mayúsculas y minúsculas tanto en los nombres de función como en los nombres de atributo deben tener o se producirá un error.

## <a name="language-definitions-and-identifiers"></a>Identificadores y definiciones de idioma
* Las funciones tienen un nombre seguido de argumentos entre paréntesis: FunctionName(argumento 1, argumento N).
* Los atributos se especifican entre corchetes: [attributeName]
* Los parámetros se identifican por signos de porcentaje: %ParameterName%
* Las constantes de cadena aparecen entre comillas: por ejemplo, "Contoso" (Nota: se deben usar comillas rectas "", no tipográficas "")
* Valores numéricos se expresan sin comillas y esperado toobe decimal. Los valores hexadecimales van precedidos de &H. Por ejemplo, 98052, &HFF
* Los valores booleanos se expresan con constantes: True, False.
* Las constantes y los literales integrados se expresan solo con su nombre: NULL, CRLF o IgnoreThisFlow

### <a name="functions"></a>Functions
El aprovisionamiento declarativo utiliza valores de muchas funciones tooenable Hola posibilidad tootransform atributo. Estas funciones se pueden anidar, por lo que el resultado de hello de una función se pasa en la función tooanother.

`Function1(Function2(Function3()))`

lista completa de Hola de funciones puede encontrarse en hello [función referencia](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>parameters
Un parámetro se define por un conector o por un administrador mediante PowerShell. Parámetros suelen contengan valores que son diferentes de sistema toosystem, por ejemplo nombre Hola de usuario de Hola Hola dominio se encuentra en. Dichos parámetros se pueden usar en flujos de atributos.

Hola conector de Active Directory proporcionado Hola parámetros siguientes para las reglas de sincronización de entrada:

| Nombre de parámetro | Comentario |
| --- | --- |
| Domain.Netbios |Formato de NetBIOS del dominio de hello está importando, por ejemplo FABRIKAMSALES |
| Domain.FQDN |Formato de nombre de dominio completo del dominio de hello está importando, por ejemplo sales.fabrikam.com |
| Domain.LDAP |Formato LDAP del dominio de hello está importando, por ejemplo, DC = ventas, DC = fabrikam, DC = com |
| Forest.Netbios |Formato de nombre de bosque de hello está importando, por ejemplo FABRIKAMCORP NetBIOS |
| Forest.FQDN |Formato FQDN del nombre de bosque de hello está importando, por ejemplo, fabrikam.com |
| Forest.LDAP |Formato LDAP del nombre de bosque de hello está importando, por ejemplo, DC = fabrikam, DC = com |

sistema de Hello proporciona Hola después de parámetro, que se tooget usado Hola identificador de hello conector está ejecutando actualmente:  
`Connector.ID`

Este es un ejemplo que rellena el dominio de atributo de metaverso Hola con el nombre de netbios de Hola de dominio Hola donde se encuentra el usuario de hello:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operadores
se puede utilizar Hola siguientes operadores:

* **Comparación**: &lt;, &lt;=, &lt;&gt;, =, &gt;, &gt;=
* **Matemáticos**: +, -, \*, -
* **Cadena**: &amp; (concatenar)
* **Lógico**: &amp;&amp; (and), || (or)
* **Orden de evaluación**: ( )

Los operadores son evaluada tooright izquierdo y tienen Hola misma prioridad de evaluación. Es decir, Hola \* (multiplicador) no se evalúa antes - (resta). 2\*(5 + 3) no es Hola igual que 2\*5 + 3. Hello paréntesis () se usan evaluación de hello toochange ordenar cuando deja tooright orden de evaluación no es adecuado.

## <a name="multi-valued-attributes"></a>Atributos con varios valores
funciones de Hello pueden operar en los atributos de un solo valor y con varios valores. Para los atributos multivalor, función hello funciona a través de cada valor y se aplica Hola la misma función tooevery valor.

Por ejemplo:  
`Trim([proxyAddresses])`Hacer un recorte de cada valor de atributo proxyAddress de Hola.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Para cada valor con un @-sign, sustituya Hola de dominios con @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Busque Hola dirección SIP y quitarlo de los valores de hello.

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información acerca del modelo de configuración de hello en [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Vea cómo declarativa usa out-of-box en el aprovisionamiento es [configuración predeterminada de descripción hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Vea cómo toomake un práctico cambiar mediante el aprovisionamiento declarativo en [cómo toomake una toohello de cambio de configuración predeterminados](active-directory-aadconnectsync-change-the-configuration.md).

**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

**Temas de referencia**

* [Azure AD Connect Sync: referencia de funciones](active-directory-aadconnectsync-functions-reference.md)

