---
title: "Conceptos de diseño de Azure AD Connect | Microsoft Docs"
description: "En este tema se detallan algunas áreas de diseño de implementación"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: conceptos de diseño
Hola de este tema sirve toodescribe áreas que deben considerarse a través durante el diseño de implementación de Hola de Azure AD Connect. Este tema trata de una profundización en determinadas áreas, y estos conceptos se describen también brevemente en otros temas.

## <a name="sourceanchor"></a>sourceAnchor
atributo de Hello sourceAnchor se define como *un atributo inmutable durante la duración de Hola de un objeto*. Identifica de forma única un objeto como Hola mismo objetos locales y en Azure AD. atributo de Hello también se denomina **immutableId** y Hola dos nombres se usan intercambiables.

word de Hello inmutable, que es "no se puede cambiar", es importante toothis tema. Puesto que el valor de este atributo no se puede cambiar después de que se ha establecido, es importante toopick un diseño que admite el escenario.

atributo de Hola se usa para hello los escenarios siguientes:

* Cuando un nuevo servidor de motor de sincronización se genera, o regenera, después de una situación de recuperación ante desastres, este atributo vincula los objetos existentes en Azure AD con los objetos locales.
* Si se mueve de un modelo de identidad sincronizados de tooa de identidad solo en la nube, este atributo permite objetos demasiado "coincidencia importante" los objetos existentes en Azure AD con objetos locales.
* Si utiliza la federación y, a continuación, este atributo junto con hello **userPrincipalName** se utiliza en hello toouniquely identificar a un usuario de notificación.

En este tema sólo se habla sobre sourceAnchor en lo referente toousers. Hello mismas reglas aplican tipos de objeto tooall, pero es solo para los usuarios que este problema suele ser un problema.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Selección de un buen atributo sourceAnchor
valor del atributo Hola debe seguir Hola siguiendo reglas:

* Debe tener una longitud de menos de 60 caracteres.
  * Los caracteres que no estén entre a-z, A-Z o 0-9 se codifican y cuentan como 3 caracteres.
* No debe contener caracteres especiales: &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Debe ser único globalmente.
* Debe ser una cadena, un entero o un número binario.
* No se debe basar en el nombre del usuario, estos cambios
* No debe distinguir mayúsculas y minúsculas; evite valores que pueden variar según el caso
* Debe asignarse cuando se crea el objeto de Hola

Si hello sourceAnchor ha seleccionado no es de tipo cadena, e tooensure de valor de atributo de hello Base64Encode conectarse de Azure AD no aparece ningún carácter especial. Si utiliza otro servidor de federación de AD FS, asegúrese de que el servidor también puede atributo de hello Base64Encode.

atributo de sourceAnchor Hola distingue mayúsculas de minúsculas. Un valor de "JuanPerez" no es Hola igual que "JuanPerez". Pero no debería tener dos objetos diferentes con solo una diferencia en mayúsculas o minúsculas.

Si tiene un solo bosque local, a continuación, atributo Hola debe usar es **objectGUID**. Se trata también de atributo de hello utilizado al usar configuración rápida en Azure AD Connect y también Hola atributo utilizado en la sincronización de directorios.

Si tiene varios bosques y no se mueven a los usuarios entre bosques y dominios, a continuación, **objectGUID** es una buena atributo toouse incluso en este caso.

Si mueve los usuarios entre bosques y dominios, debe buscar un atributo que no cambian o se puede mover con usuarios de Hola durante el movimiento de Hola. Un enfoque recomendado es toointroduce un atributo sintético. Un atributo que pueda contener algo parecido a un GUID sería adecuado. Durante la creación de objetos, se crea un nuevo GUID y se con marca de usuario de Hola. Una regla de sincronización personalizados puede crearse en toocreate de servidor de motor de sincronización de hello este valor basándose en hello **objectGUID** y actualización Hola atributo seleccionado en ADDS. Cuando se mueve el objeto de hello, asegúrese de tooalso seguro de copiar el contenido de Hola de este valor.

Otra solución es toopick un atributo existente, sabrá que no cambia. Uno de los atributos de uso más común es **employeeID**. Si considera que un atributo que contiene letras, asegúrese de que no hay que ningún caso de hello oportunidad (mayúsculas y minúsculas) puede cambiar para el valor del atributo de Hola. Atributos incorrectas que no deben usarse incluyen estos atributos con nombre de saludo del usuario de Hola. En el matrimonio o divorcio, nombre de hello es toochange esperado, lo cual no está permitido para este atributo. Esto también es uno de los motivos por qué atributos como **userPrincipalName**, **correo**, y **targetAddress** no son tooselect posible en la instalación de hello Azure AD Connect Asistente. Estos atributos también contienen Hola "@" carácter, que no se permite en hello sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Cambiar el atributo sourceAnchor de Hola
no se puede cambiar el valor del atributo sourceAnchor Hola después de que se ha creado el objeto de hello en Azure AD y se sincroniza la identidad de Hola.

Por esta razón, Hola siguientes restricciones aplica tooAzure AD Connect:

* atributo de sourceAnchor Hola solo puede establecerse durante la instalación inicial. Si se vuelve a ejecutar al Asistente para instalación de hello, esta opción es de solo lectura. Si necesita toochange esta configuración, debe desinstalar y volver a instalar.
* Si instala otro servidor de Azure AD Connect, a continuación, debe seleccionar Hola mismo atributo sourceAnchor usado como anteriormente. Si anteriormente ha estado usando DirSync y mover tooAzure AD conectarse, debe usar **objectGUID** ya que es el atributo de hello utilizada DirSync.
* Si se cambia el valor de Hola para sourceAnchor después de objeto Hola se haya exportado tooAzure AD, a continuación, Azure AD Connect sincronización produce un error y no permite más cambios en ese objeto antes de que se ha corregido el problema de Hola y Hola sourceAnchor se cambia en hello directorio de origen.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Uso de msDS-ConsistencyGuid como sourceAnchor
De forma predeterminada, Azure AD Connect (versión 1.1.486.0 y anteriores) usa objectGUID como atributo de hello sourceAnchor. objectGUID es genera en el sistema. No puede especificar su valor al crear objetos de AD locales. Como se explica en la sección [sourceAnchor](#sourceanchor), hay escenarios en los que tenga valor de sourceAnchor toospecify Hola. Si los escenarios de hello están tooyou aplicable, debe utilizar un atributo de AD configurable (por ejemplo, msDS-ConsistencyGuid) como atributo de sourceAnchor Hola.

Azure AD Connect (versión 1.1.524.0 y posterior) ahora facilita el uso de Hola de msDS-ConsistencyGuid como atributo sourceAnchor. Al utilizar esta característica, Azure AD Connect configurará automáticamente las reglas de sincronización de Hola para:

1. Usar msDS-ConsistencyGuid como atributo sourceAnchor de Hola para objetos de usuario. objectGUID se usa para otros tipos de objeto.

2. Para cualquier local usuario AD objeto cuyo atributo msDS-ConsistencyGuid no se rellena, Azure AD Connect escribe el atributo msDS-ConsistencyGuid de objectGUID valor toohello atrás en la instancia local de Active Directory. Una vez se rellena el atributo msDS-ConsistencyGuid de hello, Azure AD Connect, a continuación, exporta hello tooAzure de objeto AD.

>[!NOTE]
> Una vez un local se importa el objeto de AD en Azure AD Connect (es decir, se importó Hola espacio de conector de AD y se proyectan en hello metaverso), no se puede cambiar su valor de sourceAnchor ya. valor de sourceAnchor toospecify Hola para un dado local AD de objetos, configure el atributo msDS-ConsistencyGuid antes de que se importe en Azure AD Connect.

### <a name="permission-required"></a>Permiso necesario
Para este toowork característica, Hola AD DS cuenta usada toosynchronize con local de Active Directory debe tener permiso de atributo msDS-ConsistencyGuid escritura toohello en local de Active Directory.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>¿Cómo tooenable Hola ConsistencyGuid característica - instalación nueva
Puede habilitar el uso de Hola de ConsistencyGuid como sourceAnchor durante la instalación nuevo. En esta sección se trata la instalación rápida y personalizada con detalle.

  >[!NOTE]
  > Solo las versiones más recientes de Azure AD Connect (1.1.524.0 y después) admite Hola uso de ConsistencyGuid como sourceAnchor durante la instalación nuevo.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>¿Cómo tooenable Hola ConsistencyGuid característica
Actualmente, la característica de hello solo puede habilitarse durante la nueva instalación de Azure AD Connect solo.

#### <a name="express-installation"></a>Instalación rápida
Al instalar Azure AD Connect con el modo de Express, Asistente de Azure AD Connect de hello determina automáticamente hello más apropiado toouse de atributo como atributo de sourceAnchor hello mediante Hola siguiendo la lógica:

* En primer lugar, las consultas de Asistente de conectar hello Azure AD que utiliza el atributo de hello AD de Azure AD inquilino tooretrieve como Hola atributo sourceAnchor en la instalación de hello anterior AD Azure Connect (si existe). Si esta información está disponible, Azure AD Connect usa el atributo de hello misma instancia de AD.

  >[!NOTE]
  > Solo las versiones más recientes de Azure AD Connect (1.1.524.0 y después) almacena la información en su inquilino de Azure AD sobre el atributo sourceAnchor de hello usará durante la instalación. Las versiones anteriores de Azure AD Connect no lo hacen.

* Si no está disponible la información sobre hello sourceAnchor atributo utilizado, el Asistente de Hola comprueba el estado de hello del atributo msDS-ConsistencyGuid de hello en su Active Directory local. Si atributo hello no está configurado en cualquier objeto de directorio de hello, Asistente de hello utiliza Hola msDS-ConsistencyGuid como atributo de hello sourceAnchor. Si se configura el atributo hello en uno o más objetos de directorio hello, Asistente Hola concluye atributo Hola se está usando en otras aplicaciones y no es adecuado como atributo sourceAnchor...

* En este caso, Asistente Hola vuelve toousing objectGUID como atributo de hello sourceAnchor.

* Una vez que se decide el atributo sourceAnchor de hello, Asistente Hola almacena información de hello en el inquilino de Azure AD. Hola información se usará instalándolas futuras de Azure AD Connect.

Una vez completada la instalación rápida, el Asistente de hello le informa de qué atributo se ha detectado como atributo de delimitador de origen Hola.

![El asistente informa del atributo de AD seleccionado como sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Instalación personalizada
Al instalar Azure AD Connect con el modo personalizado, el Asistente de Azure AD Connect de hello proporciona dos opciones al configurar el atributo sourceAnchor:

![Instalación personalizada: configuración de sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Configuración | Descripción |
| --- | --- |
| Dejar que Azure administre delimitador de origen de Hola para mí | Seleccione esta opción si desea atributo de hello toopick de Azure AD para usted. Si selecciona esta opción, se aplica el Asistente de Azure AD Connect Hola mismo [lógica de selección del atributo sourceAnchor utilizada durante la instalación de Express](#express-installation). Instalación tooExpress similar, el Asistente de hello le informa de qué atributo se ha detectado como Hola atributo de delimitador de origen una vez finalizada la instalación personalizada. |
| Un atributo específico | Seleccione esta opción si desea toospecify un atributo de AD existente como atributo de hello sourceAnchor. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>¿Cómo tooenable Hola ConsistencyGuid característica - implementación existente
Si tiene una implementación de Azure AD Connect existente que está usando el objectGUID como atributo de delimitador de origen de hello, puede cambiar lo toousing ConsistencyGuid en su lugar.

>[!NOTE]
> Solo las versiones más recientes de Azure AD Connect (1.1.552.0 y después) admite la conmutación de tooConsistencyGuid ObjectGuid como atributo de delimitador de origen Hola.

tooswitch de tooConsistencyGuid objectGUID como atributo de delimitador de origen de hello:

1. Iniciar Asistente de hello Azure AD Connect y haga clic en **configurar** pantalla de toogo toohello tareas.

2. Seleccione hello **configurar delimitador de origen** opción de tareas y haga clic en **siguiente**.

   ![Habilitación de ConsistencyGuid para la implementación existente: paso 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Escriba sus credenciales de administrador de Azure AD y haga clic en **Siguiente**.

4. Asistente de Azure AD Connect analiza el estado de saludo del atributo msDS-ConsistencyGuid de hello en su Active Directory local. Si no está configurado el atributo de Hola en cualquier objeto en hello que directorio, Azure AD Connect concluye que ninguna otra aplicación está usando el atributo de Hola y es toouse seguro se como atributo de delimitador de origen de Hola. Haga clic en **siguiente** toocontinue.

   ![Habilitación de ConsistencyGuid para la implementación existente: paso 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. Hola **tooConfigure listo** pantalla, haga clic en **configurar** cambio de configuración de toomake Hola.

   ![Habilitación de ConsistencyGuid para la implementación existente: paso 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Una vez que finalice la configuración de hello, Asistente Hola indica que msDS-ConsistencyGuid ahora se usa como atributo de delimitador de origen Hola.

   ![Habilitación de ConsistencyGuid para la implementación existente: paso 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Durante el análisis de hello (paso 4), si se configura el atributo hello en uno o más objetos de directorio hello, Asistente Hola concluye atributo Hola se está usando otra aplicación y devuelve un error como se muestra en el siguiente diagrama de Hola. Si está seguro de que no utiliza ese atributo hello las aplicaciones existentes, debe toocontact soporte técnico para obtener información sobre cómo toosuppress Hola error.

![Habilitación de ConsistencyGuid para la implementación existente: error](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Repercusiones en AD FS o la configuración de la federación de terceros
Si utilizas Azure AD Connect toomanage implementación de AD FS local, hello Azure AD Connect actualiza automáticamente el atributo Hola AD mismo toouse de reglas de notificación de hello como sourceAnchor. Esto garantiza que esa notificación de ImmutableID Hola generada por AD FS es coherente con hello sourceAnchor valores exportados tooAzure AD.

Si está administrando AD FS fuera de Azure AD Connect o está usando los servidores de federación de terceros para la autenticación, debe actualizar manualmente las reglas de notificación de Hola para ImmutableID toobe notificación coherente con los valores de hello sourceAnchor exporta tooAzure AD como se describe en la sección del artículo [modificar AD FS las reglas de notificación](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Asistente de Hello devuelve Hola después de advertencia después de que finalice la instalación:

![Configuración de federación de terceros](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Agregar nueva implementación de tooexisting de directorios
Suponga que ha implementado Azure AD Connect con hello ConsistencyGuid característica habilitada, y ahora desea tooadd otra implementación de toohello de directorio. Al tratar de directorio de hello tooadd, Asistente de Azure AD Connect comprueba el estado de hello del atributo mSDS-ConsistencyGuid de hello en el directorio de Hola. Si se configura el atributo hello en uno o más objetos de directorio hello, Asistente Hola concluye atributo Hola se está usando en otras aplicaciones y devuelve un error como se muestra en el siguiente diagrama de Hola. Si está seguro de que no utiliza ese atributo hello las aplicaciones existentes, debe toocontact soporte técnico para obtener información sobre cómo toosuppress Hola error.

![Agregar nueva implementación de tooexisting de directorios](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Inicio de sesión de Azure AD
Al integrar su directorio local con Azure AD, es importante toounderstand cómo configuración de sincronización de hello puede afectar al usuario de manera Hola autentica. Azure AD usa usuario de hello tooauthenticate userPrincipalName (UPN). Sin embargo, al sincronizar los usuarios, debe elegir Hola atributo toobe utilizado para el valor de userPrincipalName con cuidado.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Atributo de Hola para userPrincipalName
Debe asegurarse de cuando seleccione atributo Hola para proporcionar el valor de Hola de toobe UPN que se usa en uno de Azure

* valores de atributo de Hello ajustarse toohello UPN sintaxis (RFC 822), debería tener el formato de Holausername@domain
* sufijo de Hello en hello tooone de coincidencias de valores de hello comprobado dominios personalizados en Azure AD

En la configuración rápida, Hola supone elección para el atributo de hello es userPrincipalName. Si el atributo userPrincipalName de hello no contiene el valor de Hola desea que su toosign a los usuarios en tooAzure, a continuación, debe elegir **instalación personalizada**.

### <a name="custom-domain-state-and-upn"></a>Estado de dominio personalizado y UPN
Es importante tooensure que hay un dominio comprobado para el sufijo UPN de Hola.

John es un usuario de "contoso.com". Desea que Juan toouse Hola UPN local john@contoso.com toosign en tooAzure después de se han sincronizado los usuarios tooyour Azure AD directorio contoso.onmicrosoft.com. toodo por lo tanto, necesita tooadd y compruebe contoso.com como un dominio personalizado en Azure AD antes de empezar Vaya a sincronizar usuarios Hola. Si el sufijo UPN de Hola de Juan, por ejemplo, contoso.com, no coincide con un dominio comprobado en Azure AD, Azure AD reemplaza el sufijo UPN de hello con contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Dominios locales no enrutables y UPN para Azure AD
Algunas organizaciones tienen dominios no enrutables, como "contoso.local" o dominios de etiqueta única simple como "contoso". No son tooverify capaz de un dominio no enrutables en Azure AD. Azure AD Connect puede sincronizar tooonly un dominio comprobado en Azure AD. Cuando se crea un directorio de Azure AD, se crea un dominio enrutable que se convierte en el dominio predeterminado para Azure SD, por ejemplo, "contoso.onmicrosoft.com". Por lo tanto, se convierte en tooverify es necesario ningún otro dominio enrutable en este escenario en caso de que no desea dominio de onmicrosoft.com de toosync toohello predeterminado.

Lectura [agregar su tooAzure de nombre de dominio personalizado Active Directory](../active-directory-add-domain.md) para obtener más información sobre cómo agregar y comprobar los dominios.

Azure AD Connect detecta si está ejecutando en un entorno de dominio no enrutable y le advertirá adecuadamente antes de que prosiga con la configuración rápida. Si trabaja en un dominio no es enrutable, es probable que dicho UPN de los usuarios de Hola Hola tienen también sufijos no enrutables. Por ejemplo, si está trabajando en contoso.local, Azure AD Connect sugiere toouse configuración personalizada en lugar de usar configuración rápida. Usar una configuración personalizada, son toospecify capaz de atributo de Hola que debe usarse como UPN toosign en tooAzure después de que los usuarios de hello están sincronizado tooAzure AD.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
