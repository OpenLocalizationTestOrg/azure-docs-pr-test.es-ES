---
title: "Azure AD Connect: solución de errores durante la sincronización | Microsoft Docs"
description: "Explica cómo solucionar los errores que aparezcan durante la sincronización con Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: aaa374d5a11ef5b5860f83a87386ff981319189f
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="troubleshooting-errors-during-synchronization"></a>Solución de errores durante la sincronización
Pueden producirse errores cuando se sincronizan datos de identidad de Windows Server Active Directory (AD DS) con Azure Active Directory (Azure AD). En este artículo se proporciona información general sobre los distintos tipos de errores de sincronización, algunos de los posibles escenarios que provocan dichos errores y las posibles maneras de corregirlos. También se incluyen los tipos de error comunes, pero puede que no cubra todos los posibles errores.

 Se supone que el lector está familiarizado con los subyacentes [conceptos de diseño de AD de Azure y Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Con la versión más reciente de Azure AD Connect \(agosto 2016 o posterior\), hay un informe de errores de sincronización disponible en [Azure Portal](https://aka.ms/aadconnecthealth) como parte de Azure AD Connect Health para la sincronización.

A partir del 1 de septiembre de 2016, la característica de [resistencia de atributos duplicados es una característica de Azure Active Directory](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) estará habilitada de manera predeterminada para todos los *nuevos* inquilinos de Azure Active Directory. Esta característica se habilitará automáticamente para los inquilinos existentes en los próximos meses.

Azure AD Connect realiza 3 tipos de operaciones desde los directorios que sincroniza: importación, sincronización y exportación. En todas estas operaciones se pueden producir errores. Este artículo se centra principalmente en los errores que se producen durante la exportación a Azure AD.

## <a name="errors-during-export-to-azure-ad"></a>Errores durante la exportación a Azure AD
La siguiente sección describe los distintos tipos de errores de sincronización que pueden producirse durante la operación de exportación a Azure AD mediante el conector de Azure AD. Este conector puede identificarse por el formato de nombre, que es "contoso.*onmicrosoft.com*".
Los errores que se producen durante la exportación a Azure AD indican que la operación \(agregar, actualizar, eliminar, etc.\) intentada por Azure AD Connect \(motor de sincronización\) en Azure Active Directory no se pudo completar.

![Información general de los errores de exportación](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Errores de coincidencia de datos
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>DESCRIPCIÓN
* Cuando Azure AD Connect \(motor de sincronización\) indica a Azure Active Directory que agregue o actualice objetos, Azure AD hace coincidir el objeto entrante que utiliza el atributo **sourceAnchor** con el atributo **immutableId** de los objetos de Azure AD. Esta se denomina una **coincidencia exacta**.
* Cuando Azure AD **no encuentra** ningún objeto que hace coincidir con el atributo **immutableId** con el atributo **sourceAnchor** del objeto entrante, antes de aprovisionar un nuevo objeto, recurre al uso de los atributos ProxyAddresses y UserPrincipalName para encontrar una coincidencia. Esta se denomina **coincidencia parcial**. La coincidencia parcial está diseñada para hacer coincidir objetos que ya están presentes en Azure AD (cuyo origen en Azure AD) con los nuevos que se van a agregar o actualizar durante la sincronización de objetos que representan la misma entidad (usuarios, grupos) de forma local.
* El error **InvalidSoftMatch** se produce cuando la coincidencia exacta no encuentra ningún objeto coincidente **Y la** coincidencia parcial encuentra un objeto coincidente, pero cuyo atributo *immutableId* tiene un valor diferente que el atributo *SourceAnchor* del objeto de entrada, lo que sugiere que el objeto coincidente se sincronizó con otro objeto de una versión local de Active Directory.

En otras palabras, para que la coincidencia parcial funcione, el objeto con el que se va a realizar no debe tener ningún valor en el atributo *immutableId*. Si algún objeto cuyo atributo *immutableId* tenga un valor genera errores de coincidencia exacta, pero satisface los criterios de coincidencia parcial, la operación provocará un error de sincronización InvalidSoftMatch.

El esquema de Azure Active Directory no permite que dos o más objetos tengan el mismo valor en los atributos siguientes. \(Esta no es una lista exhaustiva.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> La característica de [resistencia de atributos duplicados es una característica de Azure AD](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) también se está implantando como comportamiento predeterminado de Azure Active Directory.  Así se reduce el número de errores de sincronización que percibe Azure AD Connect (así como otros clientes de sincronización), lo que hace que Azure AD sea más resistente en la forma de tratar los atributos de ProxyAddresses y UserPrincipalName duplicados presentes en entornos locales de AD. Esta característica no corrige los errores de duplicación. Por consiguiente, los datos se deben seguir corrigiendo. Pero permite el aprovisionamiento de nuevos objetos que, de lo contrario, no se aprovisionarían debido a la existencia de valores duplicados en Azure AD. Esto también reducirá el número de errores de sincronización que se devuelven al cliente de sincronización.
> Si esta característica está habilitada en su inquilino, no verá errores de sincronización InvalidSoftMatch al aprovisionar nuevos objetos.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Escenarios de ejemplo para InvalidSoftMatch
1. Existen dos o más objetos cuyo atributo ProxyAddresses tiene el mismo valor en el entorno de Active Directory local. Por consiguiente, solo se aprovisiona uno en Azure AD.
2. Existen dos o más objetos cuyo atributo userPrincipalName tiene el mismo valor en el entorno de Active Directory local. Por consiguiente, solo se aprovisiona uno en Azure AD.
3. Se agregó un objeto al entorno de Active Directory local en el que el atributo ProxyAddresses tiene el mismo valor que el de un objeto existente en Azure Active Directory. El objeto agregado de forma local no se aprovisiona en Azure Active Directory.
4. Se agregó un objeto al entorno de Active Directory local en el que el atributo userPrincipalName tiene el mismo valor que el de una cuenta de Azure Active Directory. El objeto no se aprovisiona en Azure Active Directory.
5. Una cuenta sincronizada se ha movido de un bosque A a un bosque B. Azure AD Connect (motor de sincronización) usaba el atributo ObjectGUID para calcular el valor de SourceAnchor. Tras moverse el bosque, el valor de la SourceAnchor cambia. El nuevo objeto (del bosque B) no se puede sincronizar con el objeto existente en Azure AD.
6. Un objeto sincronizado se eliminó accidentalmente del entorno de Active Directory local y en Active Directory se creó un objeto nuevo para la misma entidad (por ejemplo, un usuario) sin eliminar la cuenta en Azure Active Directory. La cuenta nueva no puede sincronizarse con el objeto existente de Azure AD.
7. Azure AD Connect se desinstaló y se volvió a instalar. Durante la reinstalación, se eligió un atributo diferente como valor de SourceAnchor. Todos los objetos que se habían sincronizado previamente dejaron de estar sincronizados y apareció el error InvalidSoftMatch.

#### <a name="example-case"></a>Caso de ejemplo:
1. **Bob Smith** es un usuario sincronizado en Azure Active Directory desde el entorno de Active Directory local *contoso.com*
2. El atributo **UserPrincipalName** de Bob Smith se establece como **bobs@contoso.com**.
3. **"abcdefghijklmnopqrstuv =="** es el valor del atributo **SourceAnchor** que ha calculado Azure AD Connect mediante el atributo **objectGUID** de Bob Smith desde el entorno de Active Directory local, que es el valor del atributo **immutableId** de Bob Smith en Azure Active Directory.
4. Bob también tiene los siguientes valores en el atributo **proxyAddresses**:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Un usuario nuevo, **Bob Taylor**, se agrega al entorno de Active Directory local.
6. El atributo **UserPrincipalName** de Bob Taylor se establece como **bobt@contoso.com**.
7. **"abcdefghijkl0123456789 ==" "** es el valor del atributo **sourceAnchor** que ha calculado Azure AD Connect mediante el atributo **objectGUID** desde el entorno de Active Directory local. El objeto de Bob Taylor NO se ha sincronizado aún con Azure Active Directory.
8. Bob Taylor también tiene los siguientes valores en el atributo proxyAddresses
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Durante la sincronización, Azure AD Connect reconocerá la adición de Bob Taylor al entorno de Active Directory local y pedirá a Azure AD que realizar el mismo cambio.
10. Azure AD intentará primero la coincidencia exacta. Es decir, buscará si hay algún objeto en el que el valor de immutableId sea igual a "abcdefghijkl0123456789 ==". No se producirá la coincidencia exacta, ya que no hay ningún otro objeto de Azure AD que tenga ese valor en immutableId.
11. Luego, Azure AD intentará realizar una coincidencia parcial con Bob Taylor. Es decir, buscará si hay algún objeto en el que el valor de proxyAddresses sea igual a los tres valores, entre los que se incluye smtp:bob@contoso.com
12. Azure AD encontrará el objeto de Bob Smith que se ajusta a los criterios de coincidencia parcial. Pero este objeto tiene el valor immutableId = "abcdefghijklmnopqrstuv ==", lo que indica que este objeto se sincronizó desde otro objeto del entorno de Active Directory local. Por consiguiente, Azure AD no encuentra una coincidencia parcial con estos objetos, por lo que aparecerá el error de sincronización **InvalidSoftMatch**.

#### <a name="how-to-fix-invalidsoftmatch-error"></a>Solución del error InvalidSoftMatch
El motivo más común por el que se aparece el error InvalidSoftMatch es que dos objetos con diferentes valores de \(immutableId\) de SourceAnchor tienen el mismo valor en los atributos ProxyAddresses o UserPrincipalName, que se utilizan en el proceso de coincidencia parcial en Azure AD. Para corregir la coincidencia parcial no válida

1. Identifique los valores duplicados de proxyAddresses, userPrincipalName o de cualquier otro atributo que provocan el error. Identifique también los dos \(o más\) objetos que están implicados en el conflicto. El informe que genera [Azure AD Connect Health para sincronización](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar esos dos objetos.
2. Identifique qué objeto debe tener el valor duplicado y cuál no.
3. Quite el valor duplicado del objeto que NO debería tenerlo. Tenga en cuenta que el cambio se debe realizar en el directorio del que procede el objeto. En algunos casos, es posible que sea preciso eliminar uno de los objetos en conflicto.
4. Si el cambio lo ha realizado en el entorno de AD local, deje que Azure AD Connect lo sincronice.

Tenga en cuenta que el informe de errores de sincronización de Azure AD Connect Health para sincronización se actualiza cada 30 minutos e incluye los errores del último intento de sincronización.

> [!NOTE]
> ImmutableId, por definición, no debe cambiar mientras dure el objeto. Si Azure AD Connect no se configuró teniendo en cuenta algunos de los escenarios de la lista anterior, puede acabar en una situación en la que Azure AD Connect calcula un valor diferente de SourceAnchor para el objeto de AD que representa la misma entidad (el mismo usuario, grupo, contacto, etc.) que tiene un objeto existente de Azure AD que desea seguir utilizando.
>
>

#### <a name="related-articles"></a>Artículos relacionados
* [Atributos duplicados o no válidos evitan la sincronización de directorios en Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>DESCRIPCIÓN
Cuando Azure AD intenta realizar una coincidencia parcial de dos objetos, es posible que dos objetos de diferentes "tipos de objeto" (como, Usuario, Grupo, Contacto, etc.) tengan los mismos valores en los atributos que se utilizan para realizar la coincidencia parcial. Dado que no se permite la duplicación de estos atributos en Azure AD, la operación puede provocar un error de sincronización "ObjectTypeMismatch".

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Escenarios de ejemplo para el error ObjectTypeMismatch
* Se crea un grupo de seguridad habilitado para correo en Office 365. El administrador agrega un nuevo usuario o un contacto en el entorno de AD local (que aún no se ha sincronizado con Azure AD) con el mismo valor en el atributo ProxyAddresses que el del grupo de Office 365.

#### <a name="example-case"></a>Caso de ejemplo
1. Un administrador crea un nuevo grupo de seguridad habilitado para correo en Office 365 para el departamento de impuestos y proporciona la dirección de correo electrónico tax@contoso.com. Esta operación asigna el atributo ProxyAddresses a este grupo con el valor **smtp:tax@contoso.com**.
2. Un usuario nuevo se incorpora a Contoso.com y se crea una cuenta para él en el entorno local con el valor de proxyAddress **smtp:tax@contoso.com**
3. Cuando Azure AD Connect sincronice la nueva cuenta de usuario, aparecerá el error "ObjectTypeMismatch".

#### <a name="how-to-fix-objecttypemismatch-error"></a>Solución del error ObjectTypeMismatch
El motivo más común por el que aparece el error ObjectTypeMismatch es que dos objetos de tipo diferente (Usuario, Grupos, Contactos, etc.) tienen el mismo valor para el atributo ProxyAddresses. Para corregir el error ObjectTypeMismatch:

1. Identifique los valores duplicados de proxyAddresses (o de cualquier otro atributo) que provocan el error. Identifique también los dos \(o más\) objetos que están implicados en el conflicto. El informe que genera [Azure AD Connect Health para sincronización](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar esos dos objetos.
2. Identifique qué objeto debe tener el valor duplicado y cuál no.
3. Quite el valor duplicado del objeto que NO debería tenerlo. Tenga en cuenta que el cambio se debe realizar en el directorio del que procede el objeto. En algunos casos, es posible que sea preciso eliminar uno de los objetos en conflicto.
4. Si el cambio lo ha realizado en el entorno de AD local, deje que Azure AD Connect lo sincronice. El informe de errores de sincronización de Azure AD Connect Health para sincronización se actualiza cada 30 minutos e incluye los errores del último intento de sincronización.

## <a name="duplicate-attributes"></a>Atributos duplicados
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>DESCRIPCIÓN
El esquema de Azure Active Directory no permite que dos o más objetos tengan el mismo valor en los atributos siguientes. Es decir, cada objeto de Azure AD debe tener un valor único en estos atributos en una instancia determinada.

* ProxyAddresses
* UserPrincipalName

Si Azure AD Connect intenta agregar un objeto nuevo o actualizar un objeto existente con un valor para los atributos anteriores que ya está asignado a otro objeto de Azure Active Directory, la operación producirá el error de sincronización "AttributeValueMustBeUnique".

#### <a name="possible-scenarios"></a>Escenarios posibles:
1. El valor duplicado se asigna a un objeto ya sincronizado, que entra en conflicto con otro objeto sincronizado.

#### <a name="example-case"></a>Caso de ejemplo:
1. **Bob Smith** es un usuario sincronizado en Azure Active Directory desde el entorno de Active Directory local contoso.com.
2. El atributo **UserPrincipalName** local de Bob Smith se establece como **bobs@contoso.com**.
3. Bob también tiene los siguientes valores en el atributo **proxyAddresses**:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Un usuario nuevo, **Bob Taylor**, se agrega al entorno de Active Directory local.
5. El atributo **UserPrincipalName** de Bob Taylor se establece como **bobt@contoso.com**.
6. **Bob Taylor** también tiene los siguientes valores en el atributo **ProxyAddresses** i. smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. El objeto de Bob Taylor se sincroniza correctamente con Azure AD.
8. El administrador ha decidido actualizar el atributo **ProxyAddresses** de Bob Taylor con el siguiente valor: i. **smtp:bob@contoso.com**
9. Azure AD intentará actualizar el objeto de Bob Taylor con el valor anterior, pero se producirá un error, ya que el valor de ProxyAddresses ya está asignado a Bob Smith, por lo que aparece el error "AttributeValueMustBeUnique".

#### <a name="how-to-fix-attributevaluemustbeunique-error"></a>Solución del error AttributeValueMustBeUnique
El motivo más común por el que se aparece el error AttributeValueMustBeUnique es que dos objetos con diferentes valores de \(immutableId\) de SourceAnchor tienen el mismo valor en los atributos ProxyAddresses o UserPrincipalName. Para solucionar el error AttributeValueMustBeUnique

1. Identifique los valores duplicados de proxyAddresses, userPrincipalName o de cualquier otro atributo que provocan el error. Identifique también los dos \(o más\) objetos que están implicados en el conflicto. El informe que genera [Azure AD Connect Health para sincronización](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar esos dos objetos.
2. Identifique qué objeto debe tener el valor duplicado y cuál no.
3. Quite el valor duplicado del objeto que NO debería tenerlo. Tenga en cuenta que el cambio se debe realizar en el directorio del que procede el objeto. En algunos casos, es posible que sea preciso eliminar uno de los objetos en conflicto.
4. Si el cambio lo ha realizado en el entorno de AD local, deje que Azure AD Connect lo sincronice, ya que así se corregirá el error.

#### <a name="related-articles"></a>Artículos relacionados
-[Atributos duplicados o no válidos evitan la sincronización de directorios en Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Errores de validación de datos
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>DESCRIPCIÓN
Azure Active Directory aplica varias restricciones a los datos antes de permitir que se escriban en el directorio. Esto lo hace para garantizar que los usuarios finales obtienen las mejores experiencias posibles al usar las aplicaciones que dependen de dichos datos.

#### <a name="scenarios"></a>Escenarios
a. El valor del atributo UserPrincipalName tiene caracteres no válidos o no compatibles.
b. El atributo UserPrincipalName no sigue el formato requerido.

#### <a name="how-to-fix-identitydatavalidationfailed-error"></a>Solución del error IdentityDataValidationFailed
a. Asegúrese de que el atributo userPrincipalName tiene caracteres compatibles y el formato requerido.

#### <a name="related-articles"></a>Artículos relacionados
* [Preparación del aprovisionamiento de usuarios a Office 365 mediante la sincronización de directorios](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>DESCRIPCIÓN
Este es un caso específico, ya que se produce el error de sincronización **"FederatedDomainChangeError"** cuando el sufijo del atributo UserPrincipalName de un usuario se cambia de un dominio federado a otro.

#### <a name="scenarios"></a>Escenarios
Para un usuario sincronizado, el sufijo de UserPrincipalName se ha cambiado de un dominio federado a otro dominio federado local. Por ejemplo, *UserPrincipalName = bob@contoso.com* se ha cambiado a *UserPrincipalName = bob@fabrikam.com*.

#### <a name="example"></a>Ejemplo
1. Bob Smith, una cuenta de Contoso.com, se agrega como un nuevo usuario a Active Directory con el atributo UserPrincipalName bob@contoso.com
2. Bob pasa a otra división de Contoso.com llamada Fabrikam.com y el valor de UserPrincipalName se cambia a bob@fabrikam.com
3. Tanto contoso.com como fabrikam.com son dominios federados con Azure Active Directory.
4. El atributo userPrincipalName de Bob no se actualiza, por lo que se produce un error de sincronización de "FederatedDomainChangeError".

#### <a name="how-to-fix"></a>Solución
Si se actualizó el sufijo de UserPrincipalName de un usuario de bob@**contoso.com** a bob@**fabrikam.com**, donde tanto **contoso.com** como **fabrikam.com** son **dominios federados**, siga estos pasos para corregir el error de sincronización

1. Actualice el valor UserPrincipalName del usuario en Azure AD de bob@contoso.com a bob@contoso.onmicrosoft.com. Puede usar el siguiente comando de PowerShell con el módulo de Azure AD PowerShell:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Deje que se intente realizar la sincronización en el ciclo siguiente. Esta vez la sincronización se realizará correctamente y se actualizará el valor de UserPrincipalName de Bob a bob@fabrikam.com, como cabría esperar.

#### <a name="related-articles"></a>Artículos relacionados
* [Los cambios no son sincronizados por la herramienta de sincronización de Azure Active Directory después de cambiar el UPN de una cuenta de usuario para usar un dominio federado diferente](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>DESCRIPCIÓN
Cuando un atributo supera los límites de tamaño, longitud o recuento establecidos por el esquema de Azure Active Directory, la operación de sincronización provoca que aparezcan los errores de sincronización **LargeObject** o **ExceededAllowedLength**. Este error se produce normalmente en los siguientes atributos

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Escenarios posibles
1. El atributo userCertificate de Bob almacena demasiados certificados asignados a Bob. Entre ellos puede haber certificados antiguos que hayan expirado. El límite máximo es de 15 certificados. Para más información sobre cómo controlar los errores LargeObject con atributo userCertificate, consulte el artículo [Handling LargeObject errors caused by userCertificate attribute](active-directory-aadconnectsync-largeobjecterror-usercertificate.md) (Control de errores LargeObject causados por el atributo userCertificate).
2. El atributo userSMIMECertificate de Bob almacena demasiados certificados asignados a Bob. Entre ellos puede haber certificados antiguos que hayan expirado. El límite máximo es de 15 certificados.
3. El atributo thumbnailPhoto de Bob establecido en Active Directory es demasiado grande para sincronizarse en Azure AD.
4. Durante el rellenado automático del atributo ProxyAddresses de Active Directory, un objeto tiene muchos atributos ProxyAddresses asignados.

### <a name="how-to-fix"></a>Solución
1. Asegúrese de que el atributo que produce el error está dentro de los límites permitidos.

## <a name="related-links"></a>Vínculos relacionados
* [Buscar objetos de Active Directory en el centro de administración de Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [Consulta en Azure Active Directory un objeto mediante PowerShell de Azure Active Directory](https://msdn.microsoft.com/library/azure/jj151815.aspx)
