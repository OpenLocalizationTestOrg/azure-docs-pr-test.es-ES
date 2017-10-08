---
title: "Azure AD Connect: solución de errores durante la sincronización | Microsoft Docs"
description: "Explica cómo se producen errores de tootroubleshoot durante la sincronización con Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Solución de errores durante la sincronización
Pueden producirse errores cuando se sincronizan los datos de identidad de tooAzure de Active Directory (AD DS) de Windows Server Active Directory (Azure AD). Este artículo proporciona información general sobre los distintos tipos de errores de sincronización, algunos de los escenarios posibles Hola que provocan estos errores y posibles errores de maneras toofix Hola. Este artículo incluye tipos de errores comunes de hello y no es probable que cubran todos los errores posibles de Hola.

 En este artículo se da por supuesto Hola lector está familiarizado con hello subyacente [diseñar conceptos de AD de Azure y Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Con la versión más reciente de Hola de Azure AD Connect \(agosto de 2016 o posterior\), un informe de errores de sincronización está disponible en hello [Portal de Azure](https://aka.ms/aadconnecthealth) como parte de Azure AD Connect Health para la sincronización.

A partir del 1 de septiembre de 2016 [Azure Active Directory Duplicar atributo resistencia](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) característica se habilitará de forma predeterminada para todos los hello *nueva* inquilinos de Azure Active Directory. Esta característica se habilitará automáticamente para los inquilinos existentes en los próximos meses de Hola.

Azure AD Connect realiza 3 tipos de operaciones de mantiene en sincronización de directorios de hello: importación, la sincronización y la exportación. Errores pueden tener lugar en todas las operaciones de Hola. En este artículo se centra principalmente en errores durante la exportación tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Errores durante la exportación tooAzure AD
Pasos de la sección describen los diferentes tipos de sincronización errores que pueden producirse durante la tooAzure AD de operación de exportación de hello mediante Hola conector de Azure AD. Este conector se puede identificar mediante el formato de nombre de hello es "contoso. *onmicrosoft.com*".
Errores durante la exportación tooAzure AD indican esa operación hello \(agregar, actualizar y eliminar etc.\) lleva a cabo mediante Azure AD Connect \(motor de sincronización\) en Azure Active Directory no pudo.

![Información general de los errores de exportación](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Errores de coincidencia de datos
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Descripción
* Cuando de Azure AD Connect \(motor de sincronización\) indica a Azure Active Directory tooadd o actualización de objetos, Azure AD coincidencias Hola objeto entrante con hello **sourceAnchor** atributo toohello  **immutableId** atributos de objetos en Azure AD. Esta se denomina una **coincidencia exacta**.
* Cuando Azure AD **no encuentra** cualquier objeto que coincide con hello **immutableId** atributo con hello **sourceAnchor** atributo del objeto de entrada de hello, antes de aprovisionar un nuevo objeto, recurre toouse Hola ProxyAddresses y UserPrincipalName atributos toofind una coincidencia. Esta se denomina **coincidencia parcial**. Hello coincidencia parcial es toomatch diseñada objetos ya está presente en Azure AD (que se obtienen en Azure AD) con hello nuevos objetos que se va a agregar o actualizar durante la sincronización que representan Hola misma entidad (usuarios, grupos) de forma local.
* **InvalidSoftMatch** error se produce cuando hello coincidencia importante no encuentra cualquier objeto coincidente **AND** coincidencia parcial encuentra un objeto coincidente, pero ese objeto tiene un valor diferente de *immutableId* de Hola entrante objeto *SourceAnchor*, lo que sugiere que Hola coincidencia de objeto se sincronizó con otro objeto de Active Directory local.

En otras palabras, en orden para toowork de coincidencia parcial de hello, Hola objeto toobe soft coincide con no debe tener ningún valor para hello *immutableId*. Si cualquier otro objeto con *immutableId* conjunto con un valor da error criterios de soft-match de Hola Hola coincidencia importante pero satisfactoria, Hola operación da como resultado un error de sincronización InvalidSoftMatch.

Atributos de Azure Active Directory esquema no permite dos o más objetos toohave Hola el mismo valor de hello después. \(Esta no es una lista exhaustiva.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> [Resistencia de atributo duplicada con Azure AD atributo](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) característica también se está implantando como comportamiento predeterminado de Hola de Azure Active Directory.  Esto reducirá el número de Hola de errores de sincronización visto por Azure AD Connect (así como otros clientes de sincronización) mediante la realización de Azure AD más resistente de manera Hola controla duplicados atributos ProxyAddresses y UserPrincipalName presentes en AD local entornos. Esta característica no soluciona errores de duplicación de Hola. Por lo que los datos de hello todavía tienen toobe fijo. Pero sí permite el aprovisionamiento de nuevos objetos que están bloqueados en caso contrario, en que se va a aprovisionar debido a valores tooduplicated en Azure AD. Esto también reducirá número de Hola de errores de sincronización devolvió a toohello cliente de sincronización.
> Si esta característica está habilitada para el inquilino, no verá errores de sincronización de hello InvalidSoftMatch vistos durante el aprovisionamiento de nuevos objetos.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Escenarios de ejemplo para InvalidSoftMatch
1. Dos o más objetos con el mismo valor de atributo ProxyAddresses existe en Active Directory local de Hola. Por consiguiente, solo se aprovisiona uno en Azure AD.
2. Dos o más objetos con el mismo valor de userPrincipalName que se encuentra en Active Directory local de Hola. Por consiguiente, solo se aprovisiona uno en Azure AD.
3. Un objeto que se agregó en hello en Active Directory local con hello mismo valor del atributo ProxyAddresses que un objeto existente en Azure Active Directory. objeto de Hello agregado de forma local no obtener se aprovisiona en Azure Active Directory.
4. Un objeto que se agregó en Active Directory local con hello mismo valor del atributo userPrincipalName que una cuenta de Azure Active Directory. objeto de Hello no obtener se aprovisiona en Azure Active Directory.
5. Una cuenta sincronizada se movió de tooForest de un bosque B. Azure AD Connect (motor de sincronización) estaba usando hello toocompute de atributo ObjectGUID SourceAnchor. Después de traslado de bosques de hello, el valor de Hola de hello SourceAnchor es diferente. nuevo objeto de Hello (desde el bosque B) error toosync con objeto de hello existente en Azure AD.
6. Un objeto sincronizado se eliminaron accidentalmente en Active Directory local y un nuevo objeto que se creó en Active Directory para hello misma entidad (por ejemplo, usuario) sin eliminar la cuenta de hello en Azure Active Directory. nueva cuenta de Hello produce un error toosync con objeto de Azure AD existente Hola.
7. Azure AD Connect se desinstaló y se volvió a instalar. Durante la reinstalación de hello, se ha elegido un atributo diferente como hello SourceAnchor. Todos los objetos de Hola que hubieran sincronizado previamente habían detenido sincronizando con el error InvalidSoftMatch.

#### <a name="example-case"></a>Caso de ejemplo:
1. **Bob Smith** es un usuario sincronizado en Azure Active Directory desde el entorno de Active Directory local *contoso.com*
2. El atributo **UserPrincipalName** de Bob Smith se establece como **bobs@contoso.com**.
3. **"abcdefghijklmnopqrstuv =="** es hello **SourceAnchor** calculado por Azure AD Connect con Bob Smith **objectGUID** en Active Directory local que es hello **immutableId** de Bob Smith en Azure Active Directory.
4. Bob también tiene los siguientes valores de hello **proxyAddresses** atributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Un usuario nuevo, **Bob Taylor**, se agrega toohello en Active Directory local.
6. El atributo **UserPrincipalName** de Bob Taylor se establece como **bobt@contoso.com**.
7. **"abcdefghijkl0123456789 ==" "** es hello **sourceAnchor** calculado por Azure AD Connect con de Bob Taylor **objectGUID** del local de Active Directory. Objeto de Bob Taylor todavía no ha sincronizado tooAzure Active Directory.
8. Bob Taylor tiene Hola después de los valores de atributo proxyAddresses de Hola
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Durante la sincronización, Azure AD Connect reconocerá la adición de Hola de Bob Taylor en Active Directory local y pida Azure AD toomake Hola mismo cambio.
10. Azure AD intentará primero la coincidencia exacta. Es decir, buscará si demasiado hay cualquier objeto con hello immutableId igual "abcdefghijkl0123456789 ==". No se producirá la coincidencia exacta, ya que no hay ningún otro objeto de Azure AD que tenga ese valor en immutableId.
11. Azure AD, a continuación, intentará toosoft-match Bob Taylor. Es decir, buscará si hay tres valores a cualquier objeto con proxyAddresses igual toohellosmtp:bob@contoso.com
12. Azure AD Buscar objeto de Bob Smith toomatch Hola soft-match criterios. Pero este objeto tiene un valor Hola de immutableId = "abcdefghijklmnopqrstuv ==". lo que indica que este objeto se sincronizó desde otro objeto del entorno de Active Directory local. Por consiguiente, Azure AD no encuentra una coincidencia parcial con estos objetos, por lo que aparecerá el error de sincronización **InvalidSoftMatch**.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Cómo toofix InvalidSoftMatch error
la razón más común para hello InvalidSoftMatch error Hello es dos objetos con diferentes SourceAnchor \(immutableId\) tienen el mismo valor para los atributos de hello ProxyAddresses o UserPrincipalName, que se usan durante el saludo de Hola proceso de Soft-match en Azure AD. En orden toofix Hola a coincidencia parcial no válido

1. Identificar proxyAddresses Hola duplicado, userPrincipalName u otro valor de atributo que está provocando el error de Hola. También identifica que dos \(o más\) objetos están implicados en conflicto de Hola. Hola informe generado por [Azure AD Connect Health para la sincronización de](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar los objetos de hello dos.
2. Identificar qué objeto debe continuar toohave valor de hello duplicado y objeto que no debería.
3. Quitar el valor de hello duplicado de objeto de Hola que no debería tener ese valor. Tenga en cuenta que debe cambiar hello en directorio Hola donde se originó objeto Hola de. En algunos casos, deberá toodelete uno de los objetos de hello en conflicto.
4. Si ha realizado Hola cambiar en hello en AD local, permiten Hola de sincronización de Azure AD Connect cambiar.

Tenga en cuenta que informe de errores de sincronización en Azure AD Connect Health para la sincronización se actualiza cada 30 minutos e incluye errores Hola de intento de sincronización más reciente de Hola.

> [!NOTE]
> ImmutableId, por definición, no debería cambiar de duración de Hola de objeto Hola. Si no se configuró Azure AD Connect con algunos de los escenarios de hello en mente desde Hola por encima de la lista, puede acabar en una situación donde Azure AD Connect calcula un valor distinto de hello SourceAnchor para el objeto de hello AD que representa Hola misma entidad (mismo usuario / grupo o contacto etcetera) que tiene un objeto de AD de Azure existente que desea usar toocontinue.
>
>

#### <a name="related-articles"></a>Artículos relacionados
* [Atributos duplicados o no válidos evitan la sincronización de directorios en Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Descripción
Cuando AD Azure intenta toosoft coincidencia dos objetos, es posible que dos objetos de diferentes "tipo de objeto" (por ejemplo, usuario, grupo, póngase en contacto con etc.) tienen Hola mismo los valores de atributos de hello usan coincidencia parcial de tooperform Hola. Como no se permite la duplicación de estos atributos en Azure AD, Hola operación puede dar lugar a error de sincronización de "ObjectTypeMismatch".

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Escenarios de ejemplo para el error ObjectTypeMismatch
* Se crea un grupo de seguridad habilitado para correo en Office 365. Administrador agrega un nuevo usuario o un contacto en AD local (que no se ha sincronizado aún tooAzure AD) con el mismo valor para el atributo ProxyAddresses de Hola que Hola Office 365 de hello agrupar.

#### <a name="example-case"></a>Caso de ejemplo
1. Administrador crea un nuevo grupo de seguridad habilitados para correo en Office 365 para el departamento de impuestos de Hola y proporciona una dirección de correo electrónico como tax@contoso.com. Esto asigna el atributo de ProxyAddresses de Hola para este grupo con el valor de Hola de**smtp:tax@contoso.com**
2. Agrega un nuevo usuario Contoso.com y se crea una cuenta de usuario de Hola de forma local y proxyAddress hello como**smtp:tax@contoso.com**
3. Cuando Azure AD Connect sincronizará la nueva cuenta de usuario de hello, obtendrá errores de "ObjectTypeMismatch" Hola.

#### <a name="how-toofix-objecttypemismatch-error"></a>Cómo toofix ObjectTypeMismatch error
razón más común de Hello para el error de hello ObjectTypeMismatch es dos objetos de tipo diferente (usuarios, grupos, póngase en contacto con etc.) tienen Hola mismo valor para el atributo ProxyAddresses de Hola. En orden toofix Hola ObjectTypeMismatch:

1. Identificar Hola duplicada proxyAddresses (u otro atributo) que producen error de hello en valor. También identifica que dos \(o más\) objetos están implicados en conflicto de Hola. Hola informe generado por [Azure AD Connect Health para la sincronización de](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar los objetos de hello dos.
2. Identificar qué objeto debe continuar toohave valor de hello duplicado y objeto que no debería.
3. Quitar el valor de hello duplicado de objeto de Hola que no debería tener ese valor. Tenga en cuenta que debe cambiar hello en directorio Hola donde se originó objeto Hola de. En algunos casos, deberá toodelete uno de los objetos de hello en conflicto.
4. Si ha realizado Hola cambiar en hello en AD local, permiten Hola de sincronización de Azure AD Connect cambiar. Informe de errores de sincronización en Azure AD Connect Health para la sincronización se actualiza cada 30 minutos e incluye los errores de intento de sincronización más reciente de Hola Hola.

## <a name="duplicate-attributes"></a>Atributos duplicados
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Descripción
Atributos de Azure Active Directory esquema no permite dos o más objetos toohave Hola el mismo valor de hello después. Que es que cada objeto en Azure AD es forzada toohave un valor único de estos atributos en una instancia determinada.

* ProxyAddresses
* UserPrincipalName

Si Azure AD Connect intenta tooadd un nuevo objeto o actualiza un objeto existente con un valor para hello por encima de los atributos que ya está asignada tooanother objeto en Azure Active Directory, Hola operación da como resultado el error de sincronización de Hola "AttributeValueMustBeUnique".

#### <a name="possible-scenarios"></a>Escenarios posibles:
1. Valor duplicado es objeto ya sincronizados tooan asignado, que entra en conflicto con otro objeto sincronizado.

#### <a name="example-case"></a>Caso de ejemplo:
1. **Bob Smith** es un usuario sincronizado en Azure Active Directory desde el entorno de Active Directory local contoso.com.
2. El atributo **UserPrincipalName** local de Bob Smith se establece como **bobs@contoso.com**.
3. Bob también tiene los siguientes valores de hello **proxyAddresses** atributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Un usuario nuevo, **Bob Taylor**, se agrega toohello en Active Directory local.
5. El atributo **UserPrincipalName** de Bob Taylor se establece como **bobt@contoso.com**.
6. **Bob Taylor** tiene Hola después de valores de hello **ProxyAddresses** atributo i. smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. El objeto de Bob Taylor se sincroniza correctamente con Azure AD.
8. Administrador decidió tooupdate Bob Taylor **ProxyAddresses** atributo con el siguiente valor de hello:. **smtp:bob@contoso.com**
9. Azure AD tratará de objeto de tooupdate Bob Taylor en Azure AD con hello por encima del valor, pero que no funcionará como que ProxyAddresses valor ya está asignado tooBob Smith, que produce el error de "AttributeValueMustBeUnique".

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Cómo toofix AttributeValueMustBeUnique error
la razón más común para hello AttributeValueMustBeUnique error Hello es dos objetos con diferentes SourceAnchor \(immutableId\) tienen el mismo valor para los atributos de UserPrincipalName y Hola ProxyAddresses de Hola. En orden toofix AttributeValueMustBeUnique error

1. Identificar proxyAddresses Hola duplicado, userPrincipalName u otro valor de atributo que está provocando el error de Hola. También identifica que dos \(o más\) objetos están implicados en conflicto de Hola. Hola informe generado por [Azure AD Connect Health para la sincronización de](https://aka.ms/aadchsyncerrors) puede ayudarle a identificar los objetos de hello dos.
2. Identificar qué objeto debe continuar toohave valor de hello duplicado y objeto que no debería.
3. Quitar el valor de hello duplicado de objeto de Hola que no debería tener ese valor. Tenga en cuenta que debe cambiar hello en directorio Hola donde se originó objeto Hola de. En algunos casos, deberá toodelete uno de los objetos de hello en conflicto.
4. Si ha realizado Hola cambiar en hello en AD local, permiten Hola de sincronización de Azure AD Connect cambiar de hello error tooget fijada.

#### <a name="related-articles"></a>Artículos relacionados
-[Atributos duplicados o no válidos evitan la sincronización de directorios en Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Errores de validación de datos
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Descripción
Azure Active Directory aplica varias restricciones en los datos antes de permitir que toobe datos escrito en el directorio de Hola Hola propio. Se trata de tooensure que los usuarios finales obtienen mejores experiencias del posible Hola durante el uso de las aplicaciones de Hola que dependen de estos datos.

#### <a name="scenarios"></a>Escenarios
a. valor del atributo UserPrincipalName Hola tiene caracteres no válida o incompatible.
b. atributo UserPrincipalName de Hello no sigue el formato requerido de Hola.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Cómo toofix IdentityDataValidationFailed error
a. Asegúrese de que ese atributo userPrincipalName de Hola admite caracteres y el formato requerido.

#### <a name="related-articles"></a>Artículos relacionados
* [Preparar tooprovision a los usuarios a través de la sincronización de directorios tooOffice 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Descripción
Se trata de un caso concreto que tiene como resultado un **"FederatedDomainChangeError"** error de sincronización cuando se cambia el sufijo de Hola de UserPrincipalName de un usuario de un dominio federado tooanother de dominio federado.

#### <a name="scenarios"></a>Escenarios
Para un usuario sincronizado, sufijo de UserPrincipalName Hola se cambió de un dominio federado en tooanother de dominio federado local. Por ejemplo, *UserPrincipalName = bob@contoso.com*  cambió demasiado*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Ejemplo
1. Bob Smith, una cuenta de Contoso.com, se agrega como un nuevo usuario en Active Directory con hello UserPrincipalNamebob@contoso.com
2. Bob mueve cambia tooa otro tipo de división Contoso.com llamado Fabrikam.com y su UserPrincipalNametoobob@fabrikam.com
3. Tanto contoso.com como fabrikam.com son dominios federados con Azure Active Directory.
4. El atributo userPrincipalName de Bob no se actualiza, por lo que se produce un error de sincronización de "FederatedDomainChangeError".

#### <a name="how-toofix"></a>Cómo toofix
Si el sufijo de UserPrincipalName de un usuario se actualizó de Roberto @**contoso.com** toobob @**fabrikam.com**, donde ambos **contoso.com** y **fabrikam.com** son **los dominios federados**, a continuación, siga estos errores de sincronización de pasos toofix Hola

1. Actualizar UserPrincipalName del usuario de hello en Azure AD desde bob@contoso.com toobob@contoso.onmicrosoft.com. Puede usar Hola siguiente comando de PowerShell con hello módulo de PowerShell de Azure AD:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Permitir la sincronización de hello siguiente sincronización ciclo tooattempt. Esta sincronización de hora se realice correctamente y se actualizan Hola UserPrincipalName de Bob toobob@fabrikam.com según lo previsto.

#### <a name="related-articles"></a>Artículos relacionados
* [Los cambios no se sincronizan mediante la herramienta de sincronización de Azure Active Directory Hola después de cambiar Hola UPN de un toouse de cuenta de usuario un dominio federado diferente](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Descripción
Cuando un atributo supera Hola permitida el límite de tamaño, el límite de longitud o límite de cantidad establecida por el esquema de Active Directory de Azure, Hola sincronización operación da como resultado de hello **LargeObject** o **ExceededAllowedLength** error de sincronización. Normalmente este error se produce para los siguientes atributos de Hola

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Escenarios posibles
1. Atributo de userCertificate de Bob almacena demasiados tooBob certificados asignados. Entre ellos puede haber certificados antiguos que hayan expirado. un límite estricto Hello es 15 certificados. Para obtener más información sobre cómo toohandle LargeObject errores con userCertificate atributo, por favor, consulte tooarticle [LargeObject de control de errores por atributo userCertificate](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Atributo de Bob userSMIMECertificate almacena demasiados tooBob certificados asignados. Entre ellos puede haber certificados antiguos que hayan expirado. un límite estricto Hello es 15 certificados.
3. ThumbnailPhoto de Bob definida en Active Directory es demasiado grande toobe sincronizado en Azure AD.
4. Durante el rellenado automático de atributo ProxyAddresses de hello en Active Directory, un objeto tiene demasiadas ProxyAddresses asignados.

### <a name="how-toofix"></a>Cómo toofix
1. Asegúrese de que ese atributo Hola provocando el error de hello está dentro Hola permitida limitación.

## <a name="related-links"></a>Vínculos relacionados
* [Buscar objetos de Active Directory en el centro de administración de Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [¿Cómo tooquery Azure Active Directory para un objeto mediante Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
