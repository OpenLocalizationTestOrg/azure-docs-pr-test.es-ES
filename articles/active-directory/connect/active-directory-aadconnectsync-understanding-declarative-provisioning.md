---
title: 'Azure AD Connect: conocimiento del aprovisionamiento declarativo | Microsoft Docs'
description: "Explica el modelo configuración aprovisionamiento declarativo del hello en Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Sincronización de Azure AD Connect: conocimiento del aprovisionamiento declarativo
Este tema explica el modelo de configuración de hello en Azure AD Connect. modelo de Hola se denomina aprovisionamiento declarativo y podrá toomake un cambio de configuración con facilidad. Muchas cosas descritas en este tema son avanzadas y no son necesarias para la mayoría de los escenarios de los clientes.

## <a name="overview"></a>Información general
El aprovisionamiento declarativo es procesar objetos que proceden de un directorio de origen conectado y determina cómo deben transformarse atributos y objetos de Hola desde un origen tooa destino. Un objeto se procesa en una canalización de sincronización y canalización Hola Hola igual para las reglas entrantes y salientes. Una regla de entrada desde un metaverso toohello de espacio de conector y es una regla de salida de espacio de conector de hello metaverso tooa.

![Canalización de sincronización](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

canalización de Hello consta de varios módulos diferentes. Cada uno de ellos es responsable de un concepto de sincronización de objetos.

![Canalización de sincronización](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Origen de objeto de origen de Hola
* [Ámbito](#scope): busca todas las reglas de sincronización que están en ámbito.
* [Unión](#join): determina la relación entre el espacio conector y el metaverso.
* [Transformación](#transform): calcula cómo deben transformarse los atributos y el flujo.
* [Prioridad](#precedence): resuelve las contribuciones de atributo en conflicto.
* Destino, el objeto de destino de Hola

## <a name="scope"></a>Scope
módulo de ámbito de Hello está evaluando un objeto y determina las reglas de Hola que están en el ámbito y deben incluirse en el procesamiento de Hola. Función de los valores de atributos de hello en el objeto de hello, reglas de sincronización diferentes son toobe evaluada en el ámbito. Por ejemplo, un usuario deshabilitado sin ningún buzón de Exchange tiene reglas diferentes a las de un usuario con un buzón habilitado.  
![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

Hola ámbito se define como grupos y cláusulas. cláusulas de Hello están dentro de un grupo. Se usa un operador lógico AND entre todas las cláusulas de un grupo. Por ejemplo, (departamento = IT AND país = Dinamarca). Se usa un operador lógico OR entre los grupos.

![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
ámbito de Hello en esta imagen se debe leer como (departamento = IT y país = Dinamarca) o (país = Suecia). Si el grupo 1 o 2 del grupo es evaluado tootrue, regla de hello está en ámbito.

módulo de ámbito de Hello es compatible con las siguientes operaciones de Hola.

| Operación | Description |
| --- | --- |
| EQUAL, NOTEQUAL |Una comparación de cadenas que se evalúa como si valor es igual toohello en atributo Hola. Para los atributos con varios valores, consulte ISIN e ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Una comparación de cadenas que se evalúa como si el valor es menor que del valor de hello en el atributo de Hola. |
| CONTAINS, NOTCONTAINS |Una comparación de cadenas que se evalúa como si el valor puede encontrarse en algún lugar dentro de valor de atributo de Hola. |
| STARTSWITH, NOTSTARTSWITH |Una comparación de cadenas que se evalúa como si es el valor de a partir del valor de hello en el atributo de Hola Hola. |
| ENDSWITH, NOTENDSWITH |Una comparación de cadenas que evalúa si el valor está en el final de hello del valor de hello en el atributo de Hola. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Una comparación de cadenas que se evalúa como si el valor es mayor que la del valor de hello en el atributo de Hola. |
| ISNULL, ISNOTNULL |Evalúa si Hola atributo está ausente del objeto de Hola. Si el atributo de hello no está presente y, por tanto, null, regla de hello está en ámbito. |
| ISIN, ISNOTIN |Evalúa si el valor de hello está presente en el atributo de hello definido. Esta operación es la variación con varios valores de hello de iguales y NOTEQUAL. atributo Hola debe toobe un atributo multivalor y si no se encuentra el valor de hello en cualquiera de los valores de atributo de hello, a continuación, la regla de hello es en el ámbito. |
| ISBITSET, ISNOTBITSET |Evalúa si hay un determinado bit establecido. Por ejemplo, puede ser usado tooevaluate bits hello en userAccountControl toosee si un usuario está habilitado o deshabilitado. |
| ISMEMBEROF, ISNOTMEMBEROF |valor de Hello debe contener un grupo de tooa DN en el espacio del conector de Hola. Si el objeto de hello es un miembro del grupo de hello especificado, regla de hello está en ámbito. |

## <a name="join"></a>Unión
módulo de combinación de Hello en la canalización de sincronización de hello es responsable de localizar relación Hola entre el objeto de hello en el origen de Hola y un objeto de destino de Hola. En una regla de entrada, esta relación sería un objeto en un espacio de conector para buscar un objeto de relación tooan Hola metaverso.  
![Unión entre cs y mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
objetivo de Hello es toosee si ya hay un objeto de metaverso hello, creado por otro conector, debe estar asociado. Por ejemplo, en un recurso de la cuenta de usuario de bosque Hola Hola bosque de cuenta debe combinarse con usuario Hola Hola bosque de recursos.

Las combinaciones se utilizan principalmente en toohello juntos objetos del espacio de conector de reglas de entrada toojoin mismo objeto de metaverso.

Hola uniones se definen como uno o varios grupos. Dentro de un grupo hay cláusulas. Se usa un operador lógico AND entre todas las cláusulas de un grupo. Se usa un operador lógico OR entre los grupos. grupos de Hola se procesan por orden, de toobottom superior. Cuando un grupo encuentra exactamente una coincidencia con un objeto de destino de hello, no se evalúa ninguna otra regla de combinación. Si cero o más de un objeto se encuentra, el procesamiento continúa toohello siguiente grupo de reglas. Por este motivo, deben crearse reglas de hello en orden de Hola de más explícito primero y más aproximada al final de Hola.  
![Definición de unión](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
combinaciones de Hello en esta imagen se procesan de toobottom superior. Canalización de sincronización de hello primera ve si se encuentra una coincidencia en employeeID. De lo contrario, segunda regla de hello ve si nombre de la cuenta de hello puede ser usado toojoin Hola objetos juntos. Si no es una coincidencia o bien, regla tercera y última de hello es una coincidencia más aproximada mediante Hola nombre de usuario.

Si se han evaluado todas las reglas de unión y no hay exactamente una coincidencia, Hola **tipo de vínculo** en hello **descripción** se utiliza la página. Si esta opción se establece demasiado**aprovisionar**, a continuación, se crea un nuevo objeto de destino de Hola.  
![Aprovisionar o unir](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Un objeto solo debe tener una regla de sincronización con reglas de unión en el ámbito. Si hay varias reglas de sincronización donde se define la unión, se produce un error. La prioridad no es tooresolve usado conflictos de combinación. Un objeto debe tener una regla de unión en el ámbito de atributos tooflow con hello misma dirección de entrada/salida. Si necesita tooflow atributos toohello entrante y saliente mismo objeto, debe tener una entrada y una regla de sincronización de salida con combinación.

Combinación de salida tiene un comportamiento especial cuando intente tooprovision un espacio de conector de objeto tooa destino. atributo de Hello DN es try toofirst usa una combinación inversa. Si ya existe un objeto en el espacio de conector de destino de hello con Hola mismo DN, Hola objetos se unen.

módulo de combinación de Hola se evalúa solo una vez cuando se pone una nueva regla de sincronización en el ámbito. Cuando se unió un objeto, no se solucionará incluso si ya no satisface los criterios de combinación de Hola. Si desea toodisjoin un objeto, la regla de sincronización Hola que unido objetos Hola debe salir del ámbito.

### <a name="metaverse-delete"></a>Eliminación del metaverso
Un objeto de metaverso permanece siempre que hay una regla de sincronización en el ámbito con **tipo de vínculo** establecido demasiado**aprovisionar** o **StickyJoin**. Se usa un StickyJoin cuando un conector no se permite tooprovision un nuevo objeto de metaverso toohello, pero cuando haya unido, debe eliminarse en el origen de hello antes de elimina el objeto de metaverso Hola.

Cuando se elimina un objeto de metaverso, todos los objetos asociados a una regla de sincronización de salida marcada para **aprovisionar** están marcados para su eliminación.

## <a name="transformations"></a>Transformaciones
las transformaciones de Hello son utilizado toodefine cómo deberían fluir los atributos del destino de hello origen toohello. Hello flujos pueden tener uno de los siguientes hello **de flujo de tipos**: Direct, constante o expresión. En un flujo directo, un valor de atributo fluye tal cual, sin transformaciones adicionales. El valor especificado de un saludo de conjuntos de valor constante. Una expresión usa Hola declarativa aprovisionamiento expresión lenguaje tooexpress cómo debe aplicarse la transformación de Hola. Hola detalles de lenguaje de expresiones de Hola se encuentran en hello [descripción de lenguaje de expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) tema.

![Aprovisionar o unir](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Hola **aplicar una vez** casilla define ese Hola atributo sólo se debe establecer cuando inicialmente se crea el objeto de Hola. Por ejemplo, esta configuración puede ser tooset usado una contraseña inicial para un nuevo objeto de usuario.

### <a name="merging-attribute-values"></a>Combinación de valores de atributo
En los flujos de atributo Hola un toodetermine de configuración si hay atributos con varios valores se deben combinar desde varios conectores diferentes. es el valor predeterminado de Hello **actualización**, lo que indica que la regla de sincronización Hola con mayor prioridad debe prevalecer.

![Mezcla de tipos](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

También se pueden seleccionar los valores **Merge** y **MergeCaseInsensitive**. Estas opciones permiten valores toomerge de orígenes diferentes. Por ejemplo, puede ser los atributos de miembro o proxyAddresses de hello toomerge uso de diversos bosques diferentes. Cuando se usa esta opción, todos los sincronización las reglas de ámbito para un objeto debe usar Hola mismo tipo de combinación. No se puede definir **Update** de un conector y **Merge** de otro. Si lo intenta, recibirá un error.

Hola diferencia entre **mezcla** y **MergeCaseInsensitive** es cómo tooprocess duplicar valores de atributo. motor de sincronización de Hello asegura de que no se inserten valores duplicados en el atributo de destino de Hola. Con **MergeCaseInsensitive**, duplicar valores con solo una diferencia en caso de que no van toobe presente. Por ejemplo, no debería ver ambos "SMTP:bob@contoso.com"y"smtp:bob@contoso.com" en el atributo de destino de Hola. **Mezcla** solo examina los valores exactos de Hola y varios valores que sólo hay una diferencia en el caso podría estar presente.

Hola opción **reemplazar** es Hola igual **actualización**, pero no se utiliza.

### <a name="control-hello-attribute-flow-process"></a>Proceso de flujo de control hello atributo
Cuando varias reglas de sincronización de entrada están configurados toocontribute toohello mismo atributo de metaverso, precedencia es ganador de hello toodetermine usado. valor de hello toocontribute va la regla de sincronización Hola con prioridad más alta (valor numérico más bajo). Hola que mismo sucede para reglas de salida. regla de sincronización de Hola que tengan mayor prioridad wins y contribuir toohello de valor Hola directorio conectado.

En algunos casos, en lugar de aportar un valor, debe determinar la regla de sincronización hello, lo que el comportamiento de otras reglas. Hay algunos literales especiales que se utilizan para este caso.

Las reglas de sincronización de entrada, Hola literal **NULL** puede ser usado tooindicate que flujo hello no tiene ningún valor toocontribute. Otra regla con una prioridad más baja puede aportar un valor. Si no hay ninguna regla aporta un valor, se quita el atributo de metaverso Hola. Para una regla de salida, si **NULL** es valor final Hola después de que se han procesado todas las reglas de sincronización, a continuación, se quita el valor de hello en el directorio conectado Hola.

Hola literal **AuthoritativeNull** es similar demasiado**NULL** pero con la diferencia de Hola que ninguna regla de prioridad inferior puede aportar un valor.

Un flujo de atributo también puede usar el atributo **IgnoreThisFlow**. Es tooNULL similar en sentido Hola que indica que hay nada toocontribute. diferencia de Hello es que no elimina un valor existente en el destino de Hola. Es como si el flujo de atributo Hola nunca ha sido no existe.

Aquí tiene un ejemplo:

En *Out tooAD - implementación híbrida de Exchange del usuario* Hola siga flujo puede encontrarse:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Esta expresión debe leerse como: si se encuentra el buzón de usuario de hello en Azure AD, a continuación, flujo de atributo de Hola de tooAD de Azure AD. Si no es así, ¿fluyen nada atrás tooActive Directory. En este caso, mantendría valor existente de hello en AD.

### <a name="importedvalue"></a>ImportedValue
función de Hello ImportedValue es diferente de todas las demás funciones, ya que el nombre del atributo Hola debe incluirse entre comillas, en lugar de corchetes:  
`ImportedValue("proxyAddresses")`.

Normalmente durante la sincronización de un atributo utiliza valor esperado de hello, incluso si todavía no ha exportado todavía o se recibió un error durante la exportación ("parte superior de la torre de Hola"). Una sincronización entrante supone que un atributo que todavía no ha llegado a un directorio conectado lo alcanzará en algún momento. En algunos casos, es importante tooonly sincronizar un valor que se ha confirmado por directorio conectado de hello ("holograma y delta torre de importación").

Un ejemplo de esta función puede encontrarse en hello out-of-box regla de sincronización *en desde AD – usuario Common desde Exchange*. En Exchange híbrido, valor de hello agregada Exchange online solo se debe sincronizar cuando se haya confirmado que el valor de Hola se exportó correctamente:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Prioridad
Cuando varias reglas de sincronización intente toocontribute Hola mismo destino de toohello del valor de atributo, valor de prioridad de hello es ganador de hello toodetermine usado. regla de Hello con prioridad más alta, el valor numérico más bajo, queda atributo de hello toocontribute en un conflicto.

![Mezcla de tipos](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Esta ordenación puede ser usado toodefine más preciso flujos para un pequeño subconjunto de objetos de atributo. Por ejemplo, hello fuera-de--reglas integradas Asegúrese de que los atributos de una cuenta habilitada (**User AccountEnabled**) tienen prioridad desde otras cuentas.

Se puede definir la prioridad entre conectores. Permite los conectores con valores de toocontribute mejor los datos primero.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Hola a varios objetos del mismo espacio de conector
Si tiene varios objetos en hello mismo conector espacio toohello Unidos a un objeto de metaverso mismo, se deban ajustar la prioridad. Si varios objetos están en el ámbito de hello igual la regla de sincronización, motor de sincronización de hello no es capaz de toodetermine prioridad. Es ambigua qué objeto de origen debe contribuir Hola valor toohello metaverso. Esta configuración se notifica como ambigua incluso si los atributos de hello en el origen de hello tienen Hola mismo valor.  
![Varios objetos Unidos toohello mismo objeto de máquina virtual](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

En este escenario, necesita ámbito de hello toochange de reglas de sincronización de Hola para que objetos de origen de hello tienen reglas de sincronización diferente en el ámbito. Eso le permite toodefine diferentes precedencia.  
![Varios objetos Unidos toohello mismo objeto de máquina virtual](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información acerca del lenguaje de expresiones de hello en [descripción expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Vea cómo declarativa usa out-of-box en el aprovisionamiento es [configuración predeterminada de descripción hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Vea cómo toomake un práctico cambiar mediante el aprovisionamiento declarativo en [cómo toomake una toohello de cambio de configuración predeterminados](active-directory-aadconnectsync-change-the-configuration.md).
* Continuar tooread cómo funcionan conjuntamente los usuarios y contactos en [descripción de los usuarios y contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

**Temas de referencia**

* [Azure AD Connect Sync: referencia de funciones](active-directory-aadconnectsync-functions-reference.md)
