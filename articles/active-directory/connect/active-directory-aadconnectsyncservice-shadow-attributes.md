---
title: "atributos de la sombra de servicio de sincronización de aaaAzure AD Connect | Documentos de Microsoft"
description: "Describe cómo funcionan los atributos paralelos en el servicio de sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Atributos paralelos del servicio de sincronización de Azure AD Connect
La mayoría de los atributos se representa Hola de igual manera en Azure AD tal como están en su Active Directory local. Pero algunos atributos tienen algún tratamiento especial y el valor del atributo hello en Azure AD puede ser distinto de lo que se sincroniza en Azure AD Connect.

## <a name="introducing-shadow-attributes"></a>Introducción a los atributos paralelos
Algunos atributos tienen dos representaciones en Azure AD. Valor de hello local y un valor calculado se almacenan. Estos atributos adicionales se denominan atributos paralelos. Hola dos atributos más comunes donde verá este comportamiento son **userPrincipalName** y **proxyAddress**. cambio de Hello en valores de atributo ocurre cuando hay valores en estos atributos que representan los dominios no comprobados. Pero el motor de sincronización de hello en conectar lee valor hello en el atributo de sombra de hello lo desde su perspectiva, atributo Hola se ha confirmado por Azure AD.

No puede ver los atributos de la sombra de hello mediante Hola portal de Azure o con PowerShell. Pero concepto de hello descripción ayuda a tootroubleshoot ciertos escenarios donde el atributo de hello tiene valores diferentes en el servidor local y en la nube de Hola.

toobetter entender el comportamiento de hello, examine este ejemplo desde Fabrikam:  
![Dominios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Tienen varios sufijos UPN en su instancia de Active Directory local, pero solo se ha comprobado uno.

### <a name="userprincipalname"></a>userPrincipalName
Un usuario tiene Hola después de valores de atributo en un dominio no comprobado:

| Atributo | Valor |
| --- | --- |
| userPrincipalName local | lee.sperry@fabrikam.com |
| shadowUserPrincipalName de Azure AD | lee.sperry@fabrikam.com |
| userPrincipalName de Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

atributo userPrincipalName de Hello es valor de Hola que aparece cuando se usa PowerShell.

Puesto que el valor del atributo de hello local real se almacena en Azure AD, al comprobar el dominio fabrikam.com de hello, Azure AD actualiza el atributo userPrincipalName de hello con valor de Hola de hello shadowUserPrincipalName. No es necesario toosynchronize los cambios de Azure AD Connect para estos toobe valores actualizados.

### <a name="proxyaddresses"></a>proxyAddresses
Hola mismo proceso para incluir solo dominios comprobados también se produce para proxyAddresses, pero con alguna lógica adicional. comprobación de Hola para dominios comprobados solo se produce para los usuarios de buzón. Un usuario habilitado para correo electrónico o un contacto representan un usuario de otra organización de Exchange y puede agregar los valores en objetos de toothese proxyAddresses.

Para un usuario del buzón, de forma local o en Exchange Online, aparecen únicamente los valores para los dominios comprobados. Debería ser parecido a esto:

| Atributo | Valor |
| --- | --- |
| proxyAddresses local | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| ProxyAddresses de Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

En este caso ** smtp:abbie.spencer@fabrikam.com ** se quitó porque no se ha comprobado el dominio. Pero Exchange también agregó **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam no ha usado Lync o Skype local, pero Azure AD y Exchange Online se preparan para ello.

Esta lógica para proxyAddresses es que se hace referencia tooas **ProxyCalc**. ProxyCalc se llama con cada cambio en un usuario cuando:

- usuario de Hola se ha asignado un plan de servicio que incluya Exchange Online, incluso si no se tiene licencia de usuario de Hola para Exchange. Por ejemplo, si se asigna el usuario de Hola Hola E3 SKU de Office, pero solo se asignó SharePoint Online. Esto ocurre incluso si el buzón sigue siendo local.
- Hola atributo msExchRecipientTypeDetails tiene un valor.
- Realiza un cambio tooproxyAddresses o userPrincipalName.

ProxyCalc puede tardar algún tiempo tooprocess un cambio en un usuario y no está sincronizado con el proceso de exportación de hello Azure AD Connect.

> [!NOTE]
> Hola ProxyCalc lógica tiene algunos comportamientos adicionales para escenarios avanzados que no se documentan en este tema. Este tema está automáticamente toounderstand Hola comportamiento y documenta toda la lógica interna.

### <a name="quarantined-attribute-values"></a>Valores de atributo en cuarentena
Los atributos paralelos también se utilizan cuando hay valores de atributo duplicados. Para más información, consulte [Resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Consulte también
* [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
