---
title: "Azure AD Connect sync: configuración predeterminada de descripción Hola | Documentos de Microsoft"
description: "Este artículo describe la configuración predeterminada de hello en la sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Azure AD Connect sync: configuración predeterminada de Hola de descripción
Este artículo explica las reglas de configuración de out-of-box Hola. Documenta las reglas de Hola y cómo afectan a estas reglas de configuración de Hola. También le guía a través de la configuración predeterminada de Hola de sincronización de Azure AD Connect. objetivo de Hello es que el lector de hello entienda cómo funciona el modelo de configuración de hello, denominado aprovisionamiento declarativo, en un ejemplo del mundo real. En este artículo se da por supuesto que ya ha instalado y configurar la sincronización de Azure AD Connect con el Asistente para la instalación de Hola.

detalles de hello toounderstand del modelo de configuración de hello, leer [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Reglas de out-of-box desde local tooAzure AD
Hello expresiones siguientes se pueden encontrar en la configuración de out-of-box Hola.

### <a name="user-out-of-box-rules"></a>Reglas integradas de usuario
Estas reglas aplican también toohello tipo de objeto iNetOrgPerson.

Un objeto de usuario debe cumplir Hola después toobe sincronizado:

* Debe tener un valor de sourceAnchor.
* Después de Hola se ha creado el objeto en Azure AD, a continuación, no se puede cambiar sourceAnchor. Si el valor de hello es local modificada, Hola objeto deja de sincronizar hasta hello sourceAnchor se cambia el valor anterior de tooits back.
* Debe haber hello accountEnabled (userAccountControl) atributo rellena. Con una instancia de Active Directory local, este atributo siempre estará presente y rellenado.

Hola siguientes objetos de usuario es **no** sincronizado tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Asegúrese de muchos objetos de out-of-box en Active Directory, como la cuenta de administrador integrada hello, no están sincronizadas.
* `IsPresent([sAMAccountName]) = False`. Asegúrese de que los objetos de usuario sin el atributo sAMAccountName no estén sincronizados. Esto solo sucedería prácticamente en un dominio actualizado desde NT4.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. No sincronizar la cuenta de servicio de hello usada por la sincronización de Azure AD Connect y sus versiones anteriores.
* No sincronice las cuentas de Exchange que no funcionan en Exchange Online.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* No sincronice los objetos que no vayan a funcionar en Exchange Online.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Esta máscara de bits (& H21C07000) podrían filtrar Hola siguientes objetos:
  * Carpeta pública habilitada para correo
  * Buzón del operador del sistema
  * Buzón de la base de datos de buzones (buzón del sistema)
  * Grupo de seguridad universal (no se aplicaría a un usuario, pero existe por motivos de herencia)
  * Grupo no universal (no se aplicaría a un usuario, pero existe por motivos de herencia)
  * Plan de buzón
  * Buzón de detección
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. No sincronice ningún objeto víctima de replicación.

Hola siguiendo las reglas de atributos se aplica:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. atributo de Hello sourceAnchor no se aporta un buzón vinculado. Se supone que, si se ha encontrado un buzón vinculado, cuenta real Hola está unida más adelante.
* Exchange relacionados con los atributos solo se sincronizan si hello atributo **mailNickName** tiene un valor.
* Cuando hay varios bosques, atributos se usan en hello siguiendo el orden:
  1. Atributos relacionados en toosign (por ejemplo userPrincipalName) se han contribuido de bosque de hello con una cuenta habilitada.
  2. Atributos que pueden encontrarse en una GAL de Exchange (lista Global de direcciones) se aportan desde el bosque de hello con un buzón de Exchange.
  3. Si no se encuentra ningún buzón, estos atributos pueden provenir de cualquier bosque.
  4. Relacionados con Exchange se aportan atributos (atributos técnicos no es visibles en hello GAL) del bosque de Hola donde `mailNickname ISNOTNULL`.
  5. Si hay varios bosques que deberían cumplir una de estas reglas, a continuación, Hola orden (fecha y hora) de la creación de conectores de hello (bosques) es toodetermine usado el bosque que contribuye atributos Hola.

### <a name="contact-out-of-box-rules"></a>Reglas integradas de contacto
Un objeto de contacto debe cumplir Hola después toobe sincronizado:

* contacto de Hello debe estar habilitados para correo electrónico. Se comprueba con hello siguientes reglas:
  * `IsPresent([proxyAddresses]) = True)`. se debe rellenar el atributo proxyAddresses de Hola.
  * Una dirección de correo electrónico principal puede encontrarse en el atributo proxyAddresses de Hola o atributo de correo de Hola. Hola la presencia de un @ es tooverify usado que contenido hello es una dirección de correo electrónico. Uno de estos dos reglas debe ser evaluada tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. ¿Hay una entrada con "SMTP:" y si se produce, puede un @, se puede encontrar en la cadena de hello?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. ¿Es Hola rellena el atributo de correo y si es así, puede un @, se puede encontrar en la cadena de hello?

Hola siguientes objetos de contacto es **no** sincronizado tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Asegúrese de que ningún objeto marcado como crítico se sincronice. No debería ser ninguno con una configuración predeterminada.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Estos objetos no funcionarían en Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. No sincronice ningún objeto víctima de replicación.

### <a name="group-out-of-box-rules"></a>Reglas integradas de grupo
Un objeto de grupo debe cumplir Hola después toobe sincronizado:

* Debe tener menos de 50.000 miembros. Este recuento alcanza el número de Hola de miembros de grupo local de Hola.
  * Si tiene más miembros antes de que inicia la sincronización de hello primera vez, el grupo de hello no está sincronizado.
  * Si el número de Hola de miembros crecimiento al que se creó inicialmente, a continuación, cuando llega a 50.000 miembros que detiene la sincronización hasta que el recuento de pertenencia de hello nuevo es menor que 50.000.
  * Nota: recuento de pertenencia a 50.000 hello también se aplica por Azure AD. No está toosynchronize capaz de grupos con más miembros incluso si modifica o quita esta regla.
* Si el grupo de hello es un **grupo de distribución**, a continuación, también debe estar habilitado para correo. Consulte [Reglas integradas de contacto](#contact-out-of-box-rules) para aplicar esta regla.

Hola siguientes objetos de grupo es **no** sincronizado tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Asegúrese de muchos objetos de out-of-box en Active Directory, como grupo de administradores integrados de hello, no están sincronizadas.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Grupo heredado utilizado por DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Grupo de roles.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. No sincronice ningún objeto víctima de replicación.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>Reglas integradas de ForeignSecurityPrincipal
FSP se une demasiado "any" (\*) objeto de metaverso Hola. En realidad, esta unión solo se realiza con usuarios y grupos de seguridad. Esta configuración garantiza que se resuelvan los miembros de otro bosque y que se representen correctamente en Azure AD.

### <a name="computer-out-of-box-rules"></a>Reglas integradas de equipo
Un objeto de equipo debe cumplir Hola después toobe sincronizado:

* `userCertificate ISNOTNULL`. Solo los equipos con Windows 10 rellenarán este atributo. Todos los objetos de equipo con un valor en este atributo se sincronizan.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Descripción de escenario de reglas de out-of-box Hola
En este ejemplo, usamos una implementación con un bosque de cuentas (A), un bosque de recursos (R) y un directorio de Azure AD.

![Imagen con la descripción del escenario](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

En esta configuración, se supone que hay una cuenta habilitada en el bosque de cuenta de hello y una cuenta deshabilitada en el bosque de recursos de hello con un buzón vinculado.

Nuestro objetivo con la configuración predeterminada de hello es:

* Atributos relacionados en toosign se sincronizan desde el bosque de hello con cuenta de hello habilitado.
* Atributos que se pueden encontrar en hello GAL (lista Global de direcciones) se sincronizan desde el bosque Hola con buzón Hola. Si no se encuentra ningún buzón, se usará cualquier otro bosque.
* Si se encuentra un buzón vinculado, hello vinculado cuenta habilitada debe encontrarse para hello objeto toobe exportar tooAzure AD.

### <a name="synchronization-rule-editor"></a>Editor de reglas de sincronización
configuración de Hola se pueden ver y cambiar con la herramienta de hello Editor de reglas de sincronización (SRE) y un tooit de método abreviado puede encontrarse en el menú de inicio de Hola.

![Icono del Editor de reglas de sincronización](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Hola SRE es una herramienta del kit de recursos y se instala con sincronización de Azure AD Connect. toobe puede toostart, debe ser miembro del grupo ADSyncAdmins de Hola. Cuando se inicie, verá algo parecido a lo siguiente:

![Reglas de sincronización entrantes](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

En este panel, verá todas las reglas de sincronización creadas para su configuración. Cada línea en la tabla de hello es una regla de sincronización. toohello deja en tipos de regla, se muestran dos tipos diferentes de hello: entrante y saliente. Entrante y saliente se desde Vista Hola de metaverso Hola. Son principalmente continuo toofocus en hello reglas en esta información general de entrada. lista real de Hola de reglas de sincronización depende de esquema de hello detectado en AD. En la imagen anterior de hello, cuenta de hello bosque (fabrikamonline.com) no tiene ningún servicio, como Exchange y Lync y no hay ninguna regla de sincronización se crearon para estos servicios. Sin embargo, en el bosque de recursos de hello (res.fabrikamonline.com) Buscar reglas de sincronización para estos servicios. contenido Hola de reglas de hello es diferente según la versión de Hola detectada. Por ejemplo, en una implementación de Exchange 2013, tendremos configurados más flujos de atributo que en Exchange 2010/2007.

### <a name="synchronization-rule"></a>Regla de sincronización
Una regla de sincronización es un objeto de configuración con un conjunto de atributos que se pasan cuando se cumple una condición. También es usado toodescribe cómo un objeto en un espacio de conector es tooan relacionados de hello metaverso, conocido como **combinación** o **coincide con**. Reglas de sincronización de Hello tienen un valor de prioridad que indica cómo se relacionan con tooeach otro. Una regla de sincronización con un valor numérico menor tiene una prioridad más alta y en un conflicto de flujo de atributo, wins mayor prioridad Hola la resolución de conflictos.

Por ejemplo, mire Hola regla de sincronización **en desde AD – User AccountEnabled**. Marcar esta línea en hello SRE y seleccione **editar**.

Puesto que esta regla es una regla de out-of-box, recibirá una advertencia cuando se abre la regla de Hola. No debe realizar cualquier [cambia reglas tooout-of-box](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), por lo que se le pregunte ¿cuáles son sus intenciones. En este caso, solo desea tooview Hola regla. así que seleccione **No**.

![Advertencia del Editor de reglas de sincronización](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Una regla de sincronización tiene cuatro secciones de configuración: Descripción, Filtro de ámbito, Reglas de unión y Transformaciones.

#### <a name="description"></a>Descripción
Hola primera sección proporciona información básica como el nombre y descripción.

![Pestaña Descripción del Editor de reglas de sincronización ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

También encontrará información acerca de qué sistema conectado está relacionada con esta regla, que el tipo de objeto en hello conectado sistema a que se aplica y Hola tipo de objeto de metaverso. tipo de objeto de metaverso Hola siempre es persona sin tener en cuenta cuando el tipo de objeto de origen de hello es un usuario, iNetOrgPerson o póngase en contacto con. nunca debe cambiar el tipo de objeto de metaverso Hola por lo que se crea como un tipo genérico. Hola tipo de vínculo puede establecerse tooJoin, StickyJoin o Provision. Esta configuración funciona junto con la sección de reglas de unión de Hola y se trata más adelante.

Puede ver igualmente que esta regla de sincronización se usa para la sincronización de contraseñas. Si un usuario está en el ámbito de esta regla de sincronización, contraseña de Hola se sincroniza desde toocloud local (suponiendo que ha habilitado la característica de sincronización de contraseñas de hello).

#### <a name="scoping-filter"></a>Filtro de ámbito
Hola sección Filtro de ámbito es tooconfigure usado cuando se debe aplicar una regla de sincronización. Puesto que nombre Hola de hello regla de sincronización que está mirando indica solo debe aplicarse para usuarios habilitados, se configura el ámbito de hello ese atributo Hola AD **userAccountControl** debe no haber Hola bit 2 establecido. Cuando el motor de sincronización de hello encuentre un usuario en Active Directory, se aplica esta sincronización regla cuando **userAccountControl** se establece el valor decimal de toohello 512 (usuario normal habilitado). No se aplica la regla de hello cuando el usuario de hello tiene **userAccountControl** establecer too514 (usuario normal deshabilitado).

![Pestaña Ámbito del Editor de reglas de sincronización ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

filtro de ámbito de Hello tiene grupos y cláusulas que se pueden anidar. Una regla de sincronización tooapply deben cumplir todas las cláusulas dentro de un grupo. Cuando se definen varios grupos, se debe satisfacer al menos un grupo de hello regla tooapply. Es decir, un operador OR lógico se evalúa entre grupos y uno AND lógico, dentro de un grupo. Un ejemplo de esta configuración puede encontrarse en hello regla de sincronización saliente **Out tooAAD – Group Join**. Hay varios grupos de filtros de sincronización, por ejemplo, uno para los grupos de seguridad (`securityEnabled EQUAL True`) y otro para los de distribución (`securityEnabled EQUAL False`).

![Pestaña Ámbito del Editor de reglas de sincronización ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Esta regla es toodefine usado que grupos deben ser aprovisionado tooAzure AD. Grupos de distribución deben ser toobe habilitado para correo sincronizado con Azure AD, pero para los grupos de seguridad no es necesario un correo electrónico.

#### <a name="join-rules"></a>Reglas de unión
Hola tercera sección trata usado tooconfigure cómo relacionan los objetos en el espacio de conector de hello tooobjects Hola metaverso. Hello regla examinamos anteriormente no tiene ninguna configuración para reglas de unión, por lo que en su lugar, son toolook continuo en **en desde AD – User Join**.

![Pestaña Join rules (Reglas de unión) del Editor de reglas de sincronización ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

contenido de Hola de regla de unión de hello depende de hello coincidencia opción seleccionada en el Asistente para la instalación de Hola. Para una regla de entrada, evaluación de Hola se inicia con un objeto en el espacio de conector de origen de Hola y cada grupo de reglas de unión de Hola se evalúa en secuencia. Si un objeto de origen es toomatch evaluado exactamente un objeto en Hola metaverso usando una de las reglas de unión de hello, objetos de Hola se unen. Si se han evaluado todas las reglas y no hay ninguna coincidencia, se utiliza Hola tipo de vínculo en la página de descripción de Hola. Si esta configuración se establece demasiado**aprovisionar**, a continuación, se crea un nuevo objeto en el destino de hello, Hola metaverso. tooprovision un nuevo metaverso toohello de objeto también se denomina es demasiado**proyecto** un metaverso toohello de objeto.

reglas de unión de Hola se evalúan sólo una vez. Cuando un objeto de espacio de conector y un objeto de metaverso se unen, permanecerán combinadas como ámbito de Hola de hello regla de sincronización se siga satisfaciendo.

Cuando se evalúan reglas de sincronización, solo debe haber en el ámbito una regla de sincronización con reglas de unión definidas. Si se encuentran varias reglas de sincronización con reglas de unión para un objeto, se emite un error. Por este motivo, se recomienda hello es toohave solo una regla de sincronización con combinación definida cuando varias reglas de sincronización están en el ámbito de un objeto. En la configuración de out-of-box hello para la sincronización de Azure AD Connect, estas reglas pueden encontrarse examinando nombre hello y encuentre aquellas con palabra Hola **unir** final Hola del nombre de Hola. Una regla de sincronización sin ninguna regla de combinación definida se aplica flujos de atributo de hello cuando otra regla de sincronización unir entre sí los objetos de Hola o aprovisionar un nuevo objeto de destino de Hola.

Si observa imagen Hola anterior, puede ver esa regla Hola está tratando de toojoin **objectSID** con **msExchMasterAccountSid** (Exchange) y **msRTCSIP-OriginatorSid** () Lync), que es el esperado en una topología de bosque de recursos de la cuenta. Buscar Hola misma regla en todos los bosques. Hola, se supone que cada bosque podría ser una cuenta o un recurso de bosque. Esta configuración también funciona si tiene cuentas que residen en un solo bosque y no tiene toobe unido.

#### <a name="transformations"></a>Transformaciones
sección de transformación de Hello define todos los flujos de atributos que se aplican toohello objeto de destino cuando se unen los objetos de Hola y filtro de ámbito de Hola se cumple. Volviendo a toohello **en desde AD – User AccountEnabled** regla de sincronización, encontrará Hola siguientes transformaciones:

![Pestaña Transformaciones del Editor de reglas de sincronización ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput esta configuración en contexto, en una implementación de bosque Account-Resource, resulta toofind esperado una cuenta habilitada en el bosque de cuenta de hello y una cuenta deshabilitada en el recurso de hello del bosque con la configuración de Exchange y Lync. Hola regla de sincronización que está mirando contiene atributos de hello necesarios para el inicio de sesión y estos atributos deben fluir de bosque de Hola donde hay una cuenta habilitada. Todos estos flujos de atributo se combinan en una regla de sincronización.

Una transformación puede tener tipos diferentes: Constante, Directa y Expresión.

* En un flujo de tipo constante siempre fluirá un valor codificado. En el caso de hello anterior, siempre establece el valor de hello **True** en el atributo de metaverso Hola denominado **accountEnabled**.
* En un flujo directo siempre fluye valor Hola del atributo de hello en el atributo de destino de hello origen toohello como-es.
* Hola tercer tipo de flujo es expresión y permite configuraciones más avanzadas.

lenguaje de expresiones de Hello es VBA (Visual Basic para aplicaciones), por lo que las personas con experiencia de Microsoft Office o VBScript reconocerá el formato de saludo. Los atributos se especifican entre corchetes, [nombreAtributo]. Nombres de atributo y nombres de función distinguen mayúsculas de minúsculas, pero evalúa las expresiones de Hola Hola Editor de reglas de sincronización y mostrará una advertencia si Hola expresión no es válida. Todas las expresiones se expresan en una única línea con funciones anidadas. alimentación de hello tooshow del idioma de la configuración de hello, mostramos Hola flujo para pwdLastSet, pero con comentarios adicionales insertados:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Vea [descripción expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) para obtener más información sobre el lenguaje de expresión de Hola para flujos de atributos.

### <a name="precedence"></a>Prioridad
Han examinado algunas reglas de sincronización individuales, pero las reglas de hello trabajan juntos en la configuración de Hola. En algunos casos, se aporta un valor de atributo de varios toohello de reglas de sincronización mismo atributo de destino. En este caso, la precedencia de atributo es usado toodetermine qué atributo wins. Por ejemplo, mire Hola atributo sourceAnchor. Este atributo es un toosign capaz de atributo importante toobe en tooAzure AD. Podemos encontrar un flujo de atributos para este atributo en dos reglas de sincronización diferentes, **In from AD – User AccountEnabled** e **In from AD – User Common**. Debido tooSynchronization prioridad de la regla, atributo sourceAnchor de hello es proceden de bosque Hola con una cuenta habilitada primero cuando hay un objeto de metaverso de varios objetos toohello combinadas. Si no hay ninguna cuenta habilitada, usos de motor de sincronización de Hola Hola regla de sincronización general **en desde AD – User Common**. Esta configuración garantiza que siga habiendo un atributo sourceAnchor, incluso en las cuentas deshabilitadas.

![Reglas de sincronización entrantes](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Hola de prioridad para las reglas de sincronización se define en grupos mediante el Asistente para la instalación de Hola. Todas las reglas de un grupo tienen Hola mismo nombre, pero son directorios conectados toodifferent conectado. Asistente para la instalación de Hello proporciona reglas de hello **en desde AD – User Join** mayor prioridad y se recorre en iteración sobre todos los directorios AD conectados. A continuación, continúa a través de grupos siguientes Hola de reglas en un orden predefinido. Dentro de un grupo, se agregan reglas de Hola Hola Hola de orden que conectores se agregaron en el Asistente de Hola. Si se agrega otro conector a través del Asistente de hello, se reordenan las reglas de sincronización de Hola y reglas del nuevo conector de Hola se insertan última en cada grupo.

### <a name="putting-it-all-together"></a>Resumen
Ahora conocemos lo suficiente acerca de las reglas de sincronización toobe toounderstand capaz de cómo funciona la configuración de hello con hello diferentes reglas de sincronización. Si observa en un usuario y Hola atributos que se han contribuido toohello metaverso, se aplican las reglas de Hola Hola siguiente orden:

| Nombre | Comentario |
|:--- |:--- |
| In from AD – User Join |Regla para unir objetos del espacio del conector con el metaverso. |
| In from AD – UserAccount Enabled |Atributos necesarios para el inicio de sesión tooAzure AD y Office 365. Queremos que estos atributos de cuenta de hello habilitado. |
| In from AD – User Common from Exchange |Atributos encontrados en hello lista Global de direcciones. Suponemos que es mejor calidad de los datos Hola bosque Hola donde hemos encontrado buzón del usuario de Hola. |
| In from AD – User Common |Atributos encontrados en hello lista Global de direcciones. En caso de no encontremos un buzón, cualquier otro objeto unido puede aportar el valor de atributo de Hola. |
| In from AD – User Exchange |Solo existirá si se detecta Exchange. Hará fluir todos los atributos de Exchange de la infraestructura. |
| In from AD – User Lync |Solo existirá si se detecta Lync. Hará fluir todos los atributos de Lync de la infraestructura. |

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información acerca del modelo de configuración de hello en [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Obtener más información acerca del lenguaje de expresiones de hello en [descripción expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Seguir leyendo el funcionamiento de la configuración de out-of-box hello en [descripción de los usuarios y contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Vea cómo toomake un práctico cambiar mediante el aprovisionamiento declarativo en [cómo toomake una toohello de cambio de configuración predeterminados](active-directory-aadconnectsync-change-the-configuration.md).

**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

