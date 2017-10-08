---
title: 'Azure AD Connect: historial de versiones | Microsoft Docs'
description: "En este artículo se muestran todas las versiones de Azure AD Connect y Sincronización de Azure AD"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: historial de versiones
equipo de Azure Active Directory (Azure AD) de Hello actualiza regularmente Azure AD Connect con nuevas características y funcionalidades. No todas las adiciones son aplicables tooall audiencias.

Este artículo está diseñado toohelp realizar un seguimiento de las versiones de Hola que se han publicado y toounderstand si necesita la versión más reciente de tooupdate toohello o no.

Lista de temas relacionados:


Tema. |  Detalles
--------- | --------- |
Tooupgrade de pasos de Azure AD Connect | Distintos métodos demasiado[actualizar desde una toohello versión anterior más reciente](active-directory-aadconnect-upgrade-previous-version.md) versión de Azure AD Connect.
Permisos necesarios | Para los permisos necesarios tooapply una actualización, vea [cuentas y permisos](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Descargar| [Descarga de Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Estado: 23 de julio de 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corregido

* Se corrigió un problema que provocó la regla de sincronización de out-of-box hello toobe "Out" tooAD - ImmutableId del usuario"quitar:

  * problema de Hola se produce cuando se actualiza a Azure AD Connect, o cuando Hola opción tarea *actualizar la configuración de sincronización* en hello Azure AD Connect asistente es la configuración de la sincronización de tooupdate usa Azure AD Connect.
  
  * Esta regla de sincronización es aplicable toocustomers que ha habilitado hello [msDS-ConsistencyGuid como característica de delimitador de origen](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Esta característica se presentó en la versión 1.1.524.0 y posteriores. Cuando se quita la regla de sincronización de hello, Azure AD Connect ya no puede rellenar local el atributo ms-DS-ConsistencyGuid AD con el valor del atributo ObjectGuid Hola. No evita que se aprovisionen nuevos usuarios en Azure AD.
  
  * revisión de Hello garantiza que dicha regla de sincronización de hello ya no se quitarán durante la actualización, o durante el cambio de configuración, siempre y cuando está habilitada la característica de Hola. Para clientes existentes que se han visto afectados por este problema, Hola corrección también garantiza que esa regla de sincronización de Hola se agrega después de la actualización de la versión de toothis de Azure AD Connect.

* Se ha corregido un problema que hace que las reglas de sincronización de out-of-box toohave valor de prioridad que es inferior a 100:

  * En general, los valores de precedencia entre 0 y 99 están reservados a las reglas de sincronización personalizadas. Durante la actualización, los valores de prioridad de Hola para reglas de sincronización de out-of-box son cambios de reglas de sincronización de tooaccommodate actualizada. Debido toothis problema, las reglas de sincronización de out-of-box pueden tener asignadas el valor de prioridad que es inferior a 100.
  
  * corrección de Hello impide el problema de Hola durante la actualización. Sin embargo, no restaura los valores de prioridad de Hola para clientes existentes que se han visto afectados por el problema de Hola. Se proporciona una solución independiente en hello toohelp futuro con la restauración de Hola.

* Se corrigió un problema donde hello [pantalla de dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) en hello Azure AD Connect se muestra el Asistente para *sincronizar todos los dominios y unidades organizativas* opción como activada, incluso si está habilitado el filtrado basado en la unidad organizativa.

*   Se corrigió un problema que produjo hello [pantalla configurar particiones de directorio](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) Hola Synchronization Service Manager tooreturn un error si hello *actualizar* se hace clic en el botón. mensaje de error de Hello *"se detectó un error al actualizar los dominios: no se puede toocast objeto de tipo 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hello error se produce al nuevo dominio de AD se ha agregado tooan bosque de AD existente y que está tratando de tooupdate Azure AD conectar usando Hola botón Actualizar.

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras

* [Característica de actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) se ha expandido toosupport clientes con hello siguiendo configuraciones:
  * Ha habilitado la característica de reescritura de dispositivos de Hola.
  * Ha habilitado la característica de reescritura de grupos de Hola.
  * instalación de Hello no es una configuración rápida o una actualización de la sincronización de directorios.
  * Tiene más de 100.000 objetos en el metaverso Hola.
  * Se está conectando toomore a un único bosque. El programa de instalación rápida sólo conecta tooone bosque.
  * Hola cuenta de conector AD ya no está cuenta de hello predeterminada MSOL_.
  * servidor de Hola se establece toobe en modo de almacenamiento provisional.
  * Ha habilitado la característica de reescritura de usuario de Hola.
  
  >[!NOTE]
  >expansión de Hello ámbito de característica de actualización automática de hello afecta a los clientes con Azure AD Connect compilación 1.1.105.0 y después. Si no desea que su toobe de servidor de Azure AD Connect actualiza de forma automática, debe ejecutar el siguiente cmdlet en el servidor de Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Para obtener más información acerca de cómo habilitar/deshabilitar actualización automática, consulte tooarticle [Azure AD Connect: la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Estado: no se va a publicar. Los cambios en esta compilación se incluyen en la versión 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corregido

* Se corrigió un problema que provocó Hola out-of-box sincronización regla "fuera tooAD - ImmutableId del usuario" toobe quita cuando se actualiza la configuración de filtrado basado en la unidad organizativa. Esta regla de sincronización es necesaria para hello [msDS-ConsistencyGuid como característica de delimitador de origen](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Se corrigió un problema donde hello [pantalla de dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) en hello Azure AD Connect se muestra el Asistente para *sincronizar todos los dominios y unidades organizativas* opción como activada, incluso si está habilitado el filtrado basado en la unidad organizativa.

*   Se corrigió un problema que produjo hello [pantalla configurar particiones de directorio](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) Hola Synchronization Service Manager tooreturn un error si hello *actualizar* se hace clic en el botón. mensaje de error de Hello *"se detectó un error al actualizar los dominios: no se puede toocast objeto de tipo 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hello error se produce al nuevo dominio de AD se ha agregado tooan bosque de AD existente y que está tratando de tooupdate Azure AD conectar usando Hola botón Actualizar.

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras

* [Característica de actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) se ha expandido toosupport clientes con hello siguiendo configuraciones:
  * Ha habilitado la característica de reescritura de dispositivos de Hola.
  * Ha habilitado la característica de reescritura de grupos de Hola.
  * instalación de Hello no es una configuración rápida o una actualización de la sincronización de directorios.
  * Tiene más de 100.000 objetos en el metaverso Hola.
  * Se está conectando toomore a un único bosque. El programa de instalación rápida sólo conecta tooone bosque.
  * Hola cuenta de conector AD ya no está cuenta de hello predeterminada MSOL_.
  * servidor de Hola se establece toobe en modo de almacenamiento provisional.
  * Ha habilitado la característica de reescritura de usuario de Hola.
  
  >[!NOTE]
  >expansión de Hello ámbito de característica de actualización automática de hello afecta a los clientes con Azure AD Connect compilación 1.1.105.0 y después. Si no desea que su toobe de servidor de Azure AD Connect actualiza de forma automática, debe ejecutar el siguiente cmdlet en el servidor de Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Para obtener más información acerca de cómo habilitar/deshabilitar actualización automática, consulte tooarticle [Azure AD Connect: la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Estado: julio de 2017

>[!NOTE]
>Esta versión no es toocustomers disponible a través de la característica de conectar actualización automática de hello Azure AD.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corregido
* Se corrigió un problema con el cmdlet Hola Initialize-ADSyncDomainJoinedComputerSync que provocó el dominio comprobado Hola configurado en hello existente servicio conexión punto objeto toobe cambiado aunque sigue siendo un dominio válido. Este problema se produce cuando el inquilino de Azure AD tiene más de un dominios comprobados que pueden usarse para configurar el punto de conexión de servicio de Hola.

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras
* La reescritura de contraseñas ahora está disponible en versión preliminar con la nube de Microsoft Azure Government y Microsoft Cloud Germany. Para obtener más información sobre la compatibilidad con Azure AD Connect Hola distintas instancias de servicio, consulte tooarticle [Azure AD Connect: consideraciones especiales para instancias](active-directory-aadconnect-instances.md).

* cmdlet de Hello Initialize-ADSyncDomainJoinedComputerSync tiene ahora un nuevo parámetro opcional denominado AzureADDomain. Este parámetro permite especificar que comprobar toobe de dominio que se utiliza para configurar el punto de conexión de servicio de Hola.

### <a name="pass-through-authentication"></a>Autenticación de paso a través

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras
* nombre de Hola de agente de hello necesario para la autenticación de acceso directo se ha cambiado de *conector del Proxy de aplicación de Microsoft Azure AD* demasiado*agente de Microsoft Azure AD Connect autenticación*.

* Al habilitar la autenticación de paso a través ya no se habilita la sincronización de hash de contraseña de manera predeterminada.


## <a name="115530"></a>1.1.553.0
Estado: junio de 2017

> [!IMPORTANT]
> Se produjeron cambios en las reglas de sincronización y el esquema en esta compilación. El servicio de sincronización de Azure AD Connect activará pasos de importación completa y sincronización completa después de la actualización. A continuación se describen los detalles de los cambios de Hola. tootemporarily aplazar pasos importación completa y sincronización completa después de la actualización, consulte tooarticle [cómo toodefer completa sincronización después de la actualización](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect Sync

#### <a name="known-issue"></a>Problema conocido
* Existe un problema que afecta a los clientes que están usando el [filtrado basado en la unidad organizativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) con la sincronización de Azure AD Connect. Cuando se desplaza toohello [página dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) en Asistente de hello Azure AD Connect, se espera Hola siguiente comportamiento:
  * Si está habilitado el filtrado basado en la unidad organizativa, Hola **sincronizar seleccionados dominios y unidades organizativas** opción está seleccionada.
  * En caso contrario, Hola **sincronizar todos los dominios y unidades organizativas** opción está seleccionada.

problema que surge Hello es ese hello **sincronizar todos los dominios y unidades organizativas opción** siempre está seleccionada cuando ejecute hello asistente.  Esto sucede incluso si el filtrado basado en la unidad organizativa se ha configurado anteriormente. Antes de guardar los cambios de configuración de conexión de AAD, que seguro Hola **sincronizar dominios seleccionados y se selecciona la opción de unidades organizativas** y confirme que todas las unidades organizativas que necesitan toosynchronize se vuelvan a habilitar. De otro modo, el filtrado basado en la unidad organizativa se deshabilitará.

#### <a name="fixed-issues"></a>Problemas corregidos

* Se corrigió un problema con la escritura diferida de contraseñas que permite un tooreset Administrador de AD Azure contraseña Hola de una implementación local cuenta de usuario con privilegios de AD. problema de Hola se produce cuando Azure AD Connect se concede permiso de restablecer la contraseña de Hola a través de la cuenta con privilegios de Hola. Hola problema se trata en esta versión de Azure AD Connect no permitiendo un tooreset Administrador de AD Azure contraseña Hola de una local arbitrarias AD cuenta con privilegios de usuario a menos que el Administrador de hello es propietario de Hola de esa cuenta. Para obtener más información, consulte demasiado[4033453 documento informativo sobre seguridad](https://technet.microsoft.com/library/security/4033453).

* Se corrigió un problema relacionado con toohello [msDS-ConsistencyGuid como delimitador de origen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) característica que lleva a Azure AD Connect no reescritura tooon local el atributo msDS-ConsistencyGuid de AD. Hello problema se produce cuando hay locales en varios bosques de AD agregan tooAzure AD hello y conectar *existen identidades de usuario a través de la opción de varios directorios* está seleccionada. Cuando se usa esta configuración, las reglas de sincronización resultante de hello no rellenan el atributo de sourceAnchorBinary Hola Hola metaverso. atributo de sourceAnchorBinary Hola se utiliza como atributo de origen de hello para el atributo msDS-ConsistencyGuid. Como resultado, no se produce reescritura toohello ms DSConsistencyGuid atributo. problema de hello toofix, siguientes reglas de sincronización han sido actualizado tooensure que Hola sourceAnchorBinary atributo Hola que metaverso siempre se rellena:
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* Anteriormente, incluso si hello [msDS-ConsistencyGuid como delimitador de origen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) característica no está habilitada, hello "Out tooAD – usuario ImmutableId" regla de sincronización se sigue agregando tooAzure AD Connect. efecto de Hello es benigno y no hace que la escritura diferida de toooccur del atributo msDS-ConsistencyGuid. tooavoid confusiones, se ha agregado lógica tooensure que Hola la regla de sincronización únicamente se agrega cuando se habilita la característica de Hola.

* Se ha corregido un problema que provocó toofail de sincronización de hash de contraseña con el evento de error 611. Este problema sucede después de que uno o más controladores de dominio se hayan quitado de AD local. Al final de Hola de cada ciclo de sincronización de contraseña, Hola cookie de sincronización que se emite de forma local AD contiene identificadores de invocación de hello quita los controladores de dominio con valor USN (número de secuencia de actualización) de 0. Hola, Administrador de sincronización de contraseña es toopersist no se puede sincronización cookie contenedor USN valor de 0 y se produce un error con el evento de error 611. Durante la siguiente sincronización de hello ciclo, Hola el Administrador de sincronización de contraseña vuelve Hola última persistente cookie de sincronización que no contiene ningún valor USN de 0. Esto hace que Hola mismos cambios de contraseña toobe resincronizado. Con esta corrección, Hola, Administrador de sincronización de contraseña continúa cookie de sincronización de hello correctamente.

* Anteriormente, incluso si la actualización automática se ha deshabilitado mediante el cmdlet de hello conjunto ADSyncAutoUpgrade, Hola proceso de actualización automática continúa toocheck para la actualización de forma periódica y se basa en hello descargado instalador toohonor deshabilitación. Con esta corrección, Hola proceso de actualización automática ya no se comprueba para la actualización periódicamente. corrección de saludo se aplica automáticamente al instalador de actualización para esta versión de Azure AD Connect se ejecuta una vez.

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras

* Anteriormente, Hola [msDS-ConsistencyGuid como delimitador de origen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) característica estaba únicamente en implementaciones de toonew disponible. Ahora, está disponible tooexisting implementaciones. Más concretamente:
  * tooaccess Hola características, iniciar Asistente de hello Azure AD Connect y elija hello *delimitador de origen de actualización* opción.
  * Esta opción es tooexisting visible solo las implementaciones que usan objectGuid como atributo sourceAnchor.
  * Al configurar la opción de hello, Asistente Hola valida el estado de saludo del atributo msDS-ConsistencyGuid de hello en su Active Directory local. Si el atributo de hello no está configurado en cualquier objeto de usuario en el directorio de hello, Asistente Hola utiliza Hola msDS-ConsistencyGuid como atributo de sourceAnchor de Hola. Si se configura el atributo hello en uno o varios objetos de usuario en el directorio de Hola, Asistente Hola concluye atributo Hola se está usando en otras aplicaciones y no es adecuado como atributo sourceAnchor y no permite tooproceed de cambio de hello delimitador de origen. Si está seguro de que no utiliza ese atributo hello las aplicaciones existentes, debe toocontact soporte técnico para obtener información sobre cómo toosuppress Hola error.

* Específica demasiado**userCertificate** atributos en los objetos de dispositivo, Azure AD Connect ahora busca los valores de los certificados necesarios para [conectar dispositivos Unidos a dominio tooAzure AD para la experiencia de Windows 10](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) y filtra las Hola rest antes de sincronizar tooAzure AD. tooenable este comportamiento, regla de sincronización de out-of-box Hola "Out tooAAD - dispositivo unirse SOAInAD" se ha actualizado.

* Azure AD Connect ahora admite la reescritura de Exchange Online **cloudPublicDelegates** tooon local del atributo AD **publicDelegates** atributo. Esto habilita escenario Hola donde puede tener un buzón de Exchange Online SendOnBehalfTo derechos toousers con buzón de Exchange local. toosupport esta característica, una nueva regla de sincronización de out-of-box "Out tooAD – usuario Exchange híbrido PublicDelegates reescritura" se ha agregado. Esta regla de sincronización solo se agrega tooAzure AD conectarse cuando está habilitada la característica de implementación híbrida de Exchange.

*   Azure AD Connect ahora permite sincronizar hello **altRecipient** atributo de Azure AD. toosupport este cambio, siguiendo las reglas de sincronización de out-of-box han sido actualizado flujo de atributo tooinclude Hola necesario:
  * In from AD – User Exchange
  * Out tooAAD – ExchangeOnline de usuario
  
* Hola **cloudSOAExchMailbox** atributo Hola metaverso indica si un usuario determinado tiene buzón de Exchange Online o no. Su definición ha sido actualizada tooinclude adicionales RecipientDisplayTypes de Exchange Online como esos buzones de sala de conferencias y de equipo. tooenable este cambio, la definición de Hola de atributo de cloudSOAExchMailbox hello, que se encuentra en la regla de sincronización de out-of-box "En de AAD – usuario híbrida de Exchange", se ha actualizado desde:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello siguiente:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* Siguiente Hola agregado conjunto de funciones de X509Certificate2 compatible para crear valores de certificado de toohandle de expresiones de regla de sincronización en el atributo userCertificate de hello:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Seleccionar|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* Después de los cambios de esquema han sido introducidos tooallow clientes toocreate sincronización personalizadas reglas tooflow sAMAccountName, domainNetBios y domainFQDN para los objetos de grupo, así como distinguishedName para objetos de usuario:

  * Se han agregado tooMV esquema a los atributos siguientes:
    * Group: AccountName
    * Group: domainNetBios
    * Group: domainFQDN
    * Person: distinguishedName

  * Los atributos siguientes se han agregado tooAzure esquema conector AD:
    * Group: OnPremisesSamAccountName
    * Group: NetBiosName
    * Group: DnsDomainName
    * User: OnPremisesDistinguishedName

* Hola ADSyncDomainJoinedComputerSync cmdlet script tiene ahora un nuevo parámetro opcional denominado AzureEnvironment. parámetro Hello es usado toospecify qué Hola región inquilino de Azure Active Directory correspondiente se hospeda en. Los valores válidos son:
  * AzureCloud (predeterminado)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Unir actualizada Editor de reglas de sincronización toouse (en lugar de aprovisionar) como valor predeterminado de Hola de tipo de vínculo durante la creación de reglas de sincronización.

### <a name="ad-fs-management"></a>Administración de AD FS

#### <a name="issues-fixed"></a>Problemas corregidos

* Después de las direcciones URL son nuevos extremos de WS-Federation introducidos por la resistencia de tooimprove de Azure AD frente a interrupciones de autenticación y será local tooon agregado responder la configuración del usuario de confianza de AD FS:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* Se ha corregido un problema que provocó el valor de notificación incorrecta de toogenerate de AD FS para IssuerID. problema de Hola se produce si hay varios dominios comprobados en el inquilino de Azure AD de Hola y el sufijo de dominio de Hola de hello userPrincipalName atributo usado toogenerate Hola IssuerID notificación sea al menos 3 niveles profundidad (por ejemplo, johndoe@us.contoso.com). Hola problema se resuelve mediante la actualización de regex Hola utilizado por las reglas de notificación de Hola.

#### <a name="new-features-and-improvements"></a>Nuevas características y mejoras
* Anteriormente, la característica de administración de certificados de ADFS de hello proporcionada por Azure AD Connect sólo puede usarse con granjas de servidores de AD FS administradas a través de Azure AD Connect. Ahora, puede utilizar la característica de hello con granjas de servidores de AD FS que no están administrados mediante Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Fecha de publicación: mayo de 2017

> [!IMPORTANT]
> Se produjeron cambios en las reglas de sincronización y el esquema en esta compilación. El servicio de sincronización de Azure AD Connect activará pasos de importación completa y sincronización completa después de la actualización. A continuación se describen los detalles de los cambios de Hola.
>
>

**Problemas corregidos:**

Sincronización de Azure AD Connect

* Se ha corregido un problema que hace que toooccur actualización automática en el servidor de Azure AD Connect Hola incluso si el cliente ha deshabilitado la característica de hello con el cmdlet Set-ADSyncAutoUpgrade de Hola. Con esta corrección, Hola proceso de actualización automática en el servidor de hello todavía comprueba actualización periódicamente, pero hello instalador descargado respeta configuración de actualización automática de Hola.
* Durante la actualización en contexto de sincronización de directorios, Azure AD Connect crea un toobe de cuenta de servicio de Azure AD utilizado por el conector de hello Azure AD para sincronizar con Azure AD. Una vez creada la cuenta de hello, Azure AD Connect se autentica con Azure AD utilizando la cuenta de hello. A veces, la autenticación se produce un error debido a problemas transitorios, que a su vez hace toofail actualización de DirSync en contexto con el error *"produjo un error ejecuta tarea de configurar la sincronización AAD: AADSTS50034: toosign en esta aplicación, la cuenta de hello debe agregarse toohello xxx.onmicrosoft.com directorio."* resistencia de hello tooimprove de actualización de DirSync, Azure AD Connect ahora reintentos Hola paso de autenticación.
* Hubo un problema con la compilación 443 que provoca toosucceed de actualización de DirSync en contexto, pero no se crean perfiles de ejecución necesarios para la sincronización de directorios. Se incluye lógica de recuperación en esta compilación de Azure AD Connect. Cuando el cliente actualiza toothis compilación, Azure AD Connect detecta que faltan los perfiles de ejecución y crearlos.
* Se corrigió un problema que hace que toostart de toofail del proceso de sincronización de contraseña con 6900 de Id. de evento y error *"Un elemento con hello ya se ha agregado la misma clave"*. Este problema se produce si actualiza OU filtrado de partición de configuración de AD tooinclude de configuración. toofix este problema, la sincronización de contraseña procesar ahora sincroniza cambios de contraseña de solo las particiones de dominio de AD. Se omiten las particiones que no son de dominio, como la partición de configuración.
* Durante la instalación de Express, Azure AD Connect crea una implementación local toobe usa Hola AD conector toocommunicate local de la cuenta de AD DS AD. Anteriormente, se crea la cuenta de hello con marca PASSWD_NOTREQD hello en el atributo de Control de cuentas de usuario de hello y una contraseña aleatoria se establece en la cuenta de hello. Ahora, Azure AD Connect quita explícitamente marca de hello PASSWD_NOTREQD después de establece contraseña de hello en la cuenta de hello.
* Se corrigió un problema que provoca la actualización toofail de sincronización de directorios con error *"un interbloqueo produjo en sql server que está probando tooacquire un bloqueo de aplicación"* cuando se encuentra el atributo mailNickname de Hola Hola esquema de Active Directory local, pero no es limitado toohello clase de objeto de usuario de AD.
* Un problema que hace tooautomatically de característica de reescritura de dispositivos que se deshabiliten cuando un administrador está actualizando la configuración de sincronización de Azure AD Connect con el Asistente de Azure AD Connect fijo. Esto se debe comprobación de requisitos previos rendimiento Hola Asistente para configuración de reescritura de dispositivos existente de hello en AD local y se produce un error en la comprobación de Hola. solución de Hello es comprobación de hello tooskip si ya se ha habilitado previamente reescritura de dispositivos.
* tooconfigure OU filtrado, puede usar el Asistente de Azure AD Connect de Hola u Hola Synchronization Service Manager. Anteriormente, si utiliza el filtrado de la unidad organizativa de tooconfigure Asistente de hello Azure AD Connect, unidades organizativas nuevas que se crean después se incluyen para la sincronización de directorios. Si no desea que los nuevos toobe de unidades organizativas incluida, debe configurar la unidad organizativa mediante el filtrado Hola Synchronization Service Manager. Ahora, puede lograr Hola mismo comportamiento usando el Asistente de Azure AD Connect.
* Se ha corregido un problema que provoca que los procedimientos almacenados necesarios para toobe de Azure AD Connect creado en el esquema de Hola de hello instalar Administración, en lugar de en el esquema de dbo de Hola.
* Se ha corregido un problema que produce el atributo de ID de hello devuelto por toobe de Azure AD que se omite en hello registros de eventos de servidor de conexión de AAD. problema de Hola se produce si Azure AD Connect recibe un mensaje de redirección de Azure AD y Azure AD Connect no se puede tooconnect toohello extremo proporcionado. Hola ID se usa por toocorrelate de ingenieros de soporte técnico con los registros del lado de servicio durante la solución de problemas.
* Cuando Azure AD Connect recibe el error LargeObject de Azure AD, Azure AD Connect genera un evento con Id. de evento 6941 y mensaje *"objeto aprovisionado hello es demasiado grande. Número de Hola de valores de atributo en este objeto de recorte."* En hello mismo tiempo, Azure AD Connect también genera un evento con Id. de evento 6900 y el mensaje puede inducir a error *"Microsoft.Online.Coexistence.ProvisionRetryException: no se puede toocommunicate con Windows hello servicio Azure Active Directory."* toominimize confusión, Azure AD Connect ya no genera el evento de este último de hello cuando se recibe el error LargeObject.
* Se ha corregido un problema que hace que hello toobecome Synchronization Service Manager no responde al tratar de configuración de hello tooupdate para conector LDAP genérico.

**Nuevas características y mejoras:**

Sincronización de Azure AD Connect
* Sincronización de cambios en las reglas: Hola siguiendo la regla de sincronización se han implementado cambios:
  * Conjunto de reglas de sincronización predeterminado actualizado toonot atributos de exportación **userCertificate** y **userSMIMECertificate** si los atributos de hello tienen más de 15 valores.
  * Atributos de AD **employeeID** y **msExchBypassModerationLink** ahora se incluyen en el conjunto de reglas de sincronización de hello predeterminado.
  * Se ha quitado el atributo **photo** de AD del conjunto de reglas de sincronización predeterminado.
  * Agregar **preferredDataLocation** toohello metaverso esquema y conector de AAD. Los clientes que desean tooupdate que pueden implementar ambos atributos en Azure AD personalizado de sincronización por lo que toodo de reglas. toofind más información sobre el atributo de hello, consulte la sección de tooarticle [Azure AD Connect sync: cómo toomake una toohello de cambio predeterminado configuración - Habilitar sincronización de PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Agregar **userType** toohello metaverso esquema y conector de AAD. Los clientes que desean tooupdate que pueden implementar ambos atributos en Azure AD personalizado de sincronización por lo que toodo de reglas.

* Azure AD Connect ahora automáticamente habilita Hola uso del atributo ConsistencyGuid como atributo de delimitador de origen de Hola para local objetos de Active Directory. Además, Azure AD Connect rellena el atributo de ConsistencyGuid de hello con el valor de atributo objectGuid Hola si está vacía. Esta característica es solo la implementación de toonew es aplicable. toofind más información sobre esta característica, consulte la sección de tooarticle [Azure AD Connect: diseñar conceptos: uso de msDS-ConsistencyGuid como sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nueva solución de problemas de cmdlet Invoke-ADSyncDiagnostics ha sido agregado toohelp diagnosticar la sincronización de Hash de contraseña relacionados con problemas. Para obtener información sobre cómo usar el cmdlet de hello, consulte tooarticle [solucionar problemas de sincronización de contraseña con la sincronización de Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect ahora es compatible con carpetas públicas de sincronización habilitado para correo objetos desde AD tooAzure AD en local. Puede habilitar la característica de hello con el Asistente de Azure AD Connect en características opcionales. toofind más información sobre esta característica, consulte tooarticle [compatibilidad con Office 365 Directory según el bloqueo perimetral local correo electrónico de las carpetas públicas habilitadas](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect requiere una toosynchronize de cuenta de AD DS local AD. Anteriormente, si ha instalado Azure AD Connect utilizando el modo de Express de hello, podría proporcionar credenciales de Hola de una cuenta de administrador de organización y Azure AD Connect crearía requerida una cuenta de hello AD DS. Sin embargo, de una instalación personalizada y agregar la implementación existente de bosques tooan, era necesario tooprovide Hola cuenta AD DS en su lugar. Ahora, también tiene Hola opción tooprovide Hola credenciales de una cuenta de administrador de organización durante una instalación personalizada y dejar que Azure AD Connect a crear requiere una cuenta de hello AD DS.
* Azure AD Connect ahora es compatible con AOA de SQL. Debe habilitar AOA de SQL antes de instalar Azure AD Connect. Durante la instalación, Azure AD Connect detecta si la instancia SQL Hola proporcionada está habilitada para SQL AOA o no. Si está habilitado SQL AOA, Azure AD Connect más averigua si SQL AOA es toouse configurada la replicación sincrónica o replicación asincrónica. Al configurar el agente de escucha del grupo de disponibilidad de hello, se recomienda que establezca hello RegisterAllProvidersIP propiedad too0. Esto es porque Azure AD Connect utiliza actualmente SQL Native Client tooconnect tooSQL y SQL Native Client no admite el uso de Hola de propiedad MultiSubNetFailover.
* Si está utilizando LocalDB como base de datos de hello para el servidor de Azure AD Connect y ha alcanzado su límite de tamaño de 10 GB, Hola servicio de sincronización ya no se inicia. Anteriormente, se necesita tooperform operación ShrinkDatabase en hello LocalDB tooreclaim suficiente espacio de base de datos para toostart de servicio de sincronización de Hola. Después de que, puede usar hello toodelete Synchronization Service Manager ejecutar tooreclaim historial más espacio de base de datos. Ahora, puede utilizar toopurge de cmdlet Start-ADSyncPurgeRunHistory ejecutar datos del historial de espacio de base de datos de LocalDB tooreclaim. Además, este cmdlet admite un modo sin conexión (mediante la especificación de Hola - parámetro sin conexión) que puede usarse cuando Hola servicio de sincronización no se está ejecutando. Nota: solo puede utilizarse el modo sin conexión Hola si hello servicio de sincronización no se está ejecutando y la base de datos de hello utilizada es LocalDB.
* cantidad de Hola de tooreduce de espacio de almacenamiento necesario, Azure AD Connect ahora comprime los detalles del error de sincronización antes de almacenarlos en las bases de datos de LocalDB y SQL. Al actualizar desde una versión anterior de Azure AD Connect toothis versión, Azure AD Connect realiza una compresión de un solo uso en detalles del error de sincronización existente.
* Anteriormente, después de actualizar la configuración del filtrado de unidad organizativa, se debe ejecutar manualmente importación completa tooensure objetos existentes son correctamente incluidos y excluidos de la sincronización de directorios. Ahora, Azure AD Connect desencadena automáticamente la importación completa durante la próxima sincronización de hello ciclo. Importación completa, más solo se pueden conectores toohello aplicado AD Hola actualización afectados a. Nota: esta mejora es aplicable tooOU filtrar las actualizaciones realizadas mediante el Asistente solo de hello Azure AD Connect. No es aplicable tooOU filtrado actualización realizada con hello Synchronization Service Manager.
* Antes, el filtrado basado en grupo solo admitía usuarios, grupos y objetos de contacto. Ahora, también admite objetos de equipo.
* Antes, podía eliminar datos de espacio conector sin deshabilitar el programador de Azure AD Connect Sync. Ahora, Hola Synchronization Service Manager bloquea la eliminación de Hola de datos de espacio del conector si detecta a ese programador Hola está habilitado. Además, se devuelven una advertencia los clientes de tooinform sobre la posible pérdida de datos si se elimina Hola datos del espacio de conector.
* Anteriormente, debe deshabilitar la transcripción de PowerShell para Azure AD Connect Asistente toorun correctamente. Este problema se ha resuelto en parte. Puede habilitar la transcripción de PowerShell si usas la configuración de sincronización de Azure AD Connect Asistente toomanage. Debe deshabilitar la transcripción de PowerShell si usas la configuración de AD FS del toomanage de Asistente de Azure AD Connect.



## <a name="114860"></a>1.1.486.0
Fecha de publicación: abril de 2017

**Problemas corregidos:**
* Se ha corregido el problema de hello en Azure AD Connect no se instalará correctamente en una versión localizada de Windows Server.

## <a name="114840"></a>1.1.484.0
Fecha de publicación: abril de 2017

**Problemas conocidos**:

* Esta versión de Azure AD Connect no se instalará correctamente si Hola condiciones siguientes es verdaderas todas:
   1. Realiza una actualización de DirSync o una instalación nueva de Azure AD Connect.
   2. Está utilizando una versión localizada de Windows Server donde nombre hello del grupo de administradores integrado en el servidor de hello no "Administradores".
   3. Utilizas predeterminado Hola SQL Server 2012 Express LocalDB instalada con Azure AD Connect en lugar de proporcionar su propio SQL completa.

**Problemas corregidos:**

Sincronización de Azure AD Connect
* Se ha corregido un problema donde programador de sincronización de hello omite el paso de sincronización completa de hello si uno o varios conectores no tienen perfil de ejecución para ese paso de sincronización. Por ejemplo, agregar manualmente un conector mediante Hola Synchronization Service Manager sin crear una importación diferencial perfil de ejecución para él. Esta revisión garantiza que ese programador de sincronización de hello continúa toorun importación diferencial para los demás conectores.
* Se corrigió un problema donde hello servicio de sincronización detiene inmediatamente el procesamiento un perfil de ejecución cuando es encuentra un problema con uno de los pasos de hello ejecutar. Esta revisión garantiza que Hola omite de servicio de sincronización que se ejecutan paso y continúa tooprocess Hola rest. Por ejemplo, tiene un perfil de ejecución de importación diferencial para el conector AD con varios pasos de ejecución (uno para cada dominio de Active Directory local). Hola servicio de sincronización ejecutará importación diferencial con hello otros dominios de Active Directory incluso si uno de ellos tiene problemas de conectividad de red.
* Se ha corregido un problema que hace que toobe de actualización de conector de Azure AD Hola omitido durante la actualización automática.
* Se corrigió un problema que tooincorrectly de causas AD Azure Connect determinar si el servidor de hello es un controlador de dominio durante la instalación, que a su vez causas DirSync actualizar toofail.
* Fijo un problema que hace que DirSync toonot de actualización en contexto crear cualquier perfil para hello conector de Azure AD de ejecución.
* Se ha corregido un problema donde interfaz de usuario de hello Synchronization Service Manager deja de responder al intentar tooconfigure conector LDAP genérico.

Administración de AD FS
* Se ha corregido un problema donde Asistente de Azure AD Connect de Hola se produce un error si se ha movido tooanother server nodo principal de hello AD FS.

SSO de escritorio
* Se corrigió un problema en el Asistente de Azure AD Connect de Hola donde hello pantalla de inicio de sesión no le permite habilitar la característica de escritorio SSO si ha elegido la sincronización de contraseña como opción de inicio de sesión durante la instalación nuevo.

**Nuevas características y mejoras:**

Sincronización de Azure AD Connect
* Sincronización de conectarse de Azure AD admite ahora el uso de Hola de cuenta de servicio Virtual, cuenta de servicio administrada y cuenta de servicio administrada de grupo como su cuenta de servicio. Esto aplica toonew instalación de Azure AD Connect solo. Al instalar Azure AD Connect:
    * De forma predeterminada, el Asistente para Azure AD Connect creará una cuenta de servicio virtual y la utilizará como su cuenta de servicio.
    * Si va a instalar en un controlador de dominio, Azure AD Connect vuelve tooprevious comportamiento donde se creará una cuenta de usuario de dominio y se utiliza como su cuenta de servicio.
    * Puede invalidar el comportamiento predeterminado de hello proporcionando uno de los siguientes hello:
      * Una cuenta de servicio administrada de grupo
      * Una cuenta de servicio administrada
      * Una cuenta de usuario de dominio
      * Una cuenta de usuario local
* Anteriormente, si actualiza tooa nueva compilación de Azure AD Connect que contenga los conectores actualizar o cambios de reglas de sincronización, Azure AD Connect desencadenarán un ciclo de sincronización completa. Ahora, Azure AD Connect desencadena selectivamente el paso de importación completa solo para los conectores con actualización y el paso de sincronización completa solo para los conectores con cambios de la regla de sincronización.
* Anteriormente, Hola exportar el umbral de eliminación solo aplica tooexports que se desencadena a través de programador de sincronización de Hola. Ahora, la característica de Hola se extiende exportaciones tooinclude desencadenadas manualmente por el cliente de hello mediante Hola Synchronization Service Manager.
* En su inquilino de Azure AD, hay una configuración del servicio que indica si la característica de sincronización de contraseña está habilitada para el inquilino o no. Anteriormente, es fácil toobe de configuración de servicio de hello configurado incorrectamente, Azure AD Connect cuando tenga un activo y un servidor de ensayo. Ahora, Azure AD Connect intentará tookeep de configuración del servicio Hola coherente con su active sólo para el servidor Azure AD Connect.
* El Asistente para Azure AD Connect ahora detecta y devuelve una advertencia si la instancia de AD local no tiene la papelera de reciclaje de AD habilitada.
* Anteriormente, exportación tooAzure AD tiempo de espera y se produce un error si Hola combina el tamaño de los objetos de hello en lote Hola supera cierto umbral. Ahora, Hola servicio de sincronización volverá a intentar la tooresend objetos de hello en lotes más pequeños, independientes si se encuentra el problema de Hola.
* Hola aplicación de administración de claves del servicio de sincronización se quitó del menú Inicio de Windows. Administración de clave de cifrado seguirá toobe admitido a través de la interfaz de línea de comandos mediante miiskmu.exe. Para obtener información acerca de cómo administrar clave de cifrado, consulte tooarticle [clave de cifrado de Abandoning hello Azure AD Sync conectarse](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Anteriormente, si cambia la contraseña de la cuenta de servicio de sincronización de hello Azure AD Connect, Hola servicio de sincronización no será capaz de inicio correctamente hasta que haya abandonado la clave de cifrado de Hola y reinicializar la contraseña de la cuenta de servicio de sincronización de hello Azure AD Connect. Ahora, esto ya no es necesario.

SSO de escritorio

* Asistente de Azure AD Connect ya no requiere el puerto 9090 toobe abierto en la red de hello al configurar la autenticación de paso a través y SSO de escritorio. Solo se requiere el puerto 443. 

## <a name="114430"></a>1.1.443.0
Fecha de publicación: marzo de 2017

**Problemas corregidos:**

Sincronización de Azure AD Connect
* Se ha corregido un problema que hace que Azure AD Connect Asistente toofail si Hola nombre para mostrar de hello conector de Azure AD no contener Hola inicial onmicrosoft.com dominio asignado toohello Azure AD inquilino.
* Se ha corregido un problema que hace que Azure AD Connect Asistente toofail al realizar la base de datos de conexión tooSQL cuando contraseña Hola de cuenta de servicio de sincronización de hello contiene caracteres especiales, como el apóstrofo, una coma y un espacio.
* Se corrigió un problema que produce error de hello toooccur "hello dimage tiene un delimitador que es diferente de la imagen de Hola" en un servidor de Azure AD Connect en modo de almacenamiento provisional, una vez que haya temporalmente excluido en local AD del objeto de sincronización y, a continuación, incluido lo nuevo para Vaya a sincronizar.
* Se corrigió un problema que produce error de hello toooccur "encuentra DN de objeto de hello es un fantasma" en un servidor de Azure AD Connect en modo de almacenamiento provisional, una vez que haya temporalmente excluido en local AD del objeto de sincronización y, a continuación, incluye lo nuevo para la sincronización.

Administración de AD FS
* Se ha corregido un problema donde los Asistente de Azure AD Connect no actualizar la configuración de AD FS y establece Hola derecho notificaciones en hello confianza para usuario autenticado después de configurar el Id. de inicio de sesión alternativo.
* Se ha corregido un problema donde Asistente de Azure AD Connect es servidores de toocorrectly no se puede identificador AD FS cuyas cuentas de servicio se configuran mediante formato userPrincipalName en lugar de formato de sAMAccountName.

Autenticación de paso a través
* Se ha corregido un problema que hace que Azure AD Connect Asistente toofail si pasar a través de la autenticación está seleccionada, pero se produce un error en el registro de su conector.
* Se ha corregido un problema que hace que la validación de toobypass asistente comprueba en el método de inicio de sesión seleccionado cuando se habilita la característica de SSO de escritorio de Azure AD Connect.

Restablecimiento de contraseña
* Se corrigió un problema que puede provocar hello Azure AAD Connect server toonot intento toore-conectarse si se cancela la conexión de Hola por un firewall o proxy.

**Nuevas características y mejoras:**

Sincronización de Azure AD Connect
* El cmdlet Get-ADSyncScheduler ahora devuelve una nueva propiedad booleana denominada "SyncCycleInProgress". Si Hola devolvió el valor es true, significa que hay un ciclo de sincronización programada en curso.
* Se ha movido la carpeta de destino para almacenar la instalación de Azure AD Connect y los registros de instalación de archivos de registro de toohello de %localappdata%\AADConnect too%programdata%\AADConnect tooimprove accesibilidad.

Administración de AD FS
* Se agregó compatibilidad para actualizar el certificado SSL de granja de servidores de AD FS.
* Se agregó compatibilidad para administrar AD FS 2016.
* Ahora puede especificar gMSA existente (cuenta de servicio administrada de grupo) durante la instalación de AD FS.
* Ahora puede configurar SHA-256 como algoritmo de hash de firma de Hola de confianza para usuario autenticado de Azure AD.

Restablecimiento de contraseña
* Se ha introducido mejoras tooallow Hola producto toofunction en entornos con reglas de firewall más estrictas.
* Conexión mejorada confiabilidad tooAzure Bus de servicio.

## <a name="113800"></a>1.1.380.0
Fecha de publicación: diciembre de 2016

**Problema corregido:**

* Problema de hello fijo donde hello issuerid de reglas de notificaciones para los servicios de federación de Active Directory (AD FS) es que faltan en esta compilación.

>[!NOTE]
>Esta versión no es toocustomers disponible a través de la característica de conectar actualización automática de hello Azure AD.

## <a name="113710"></a>1.1.371.0
Fecha de publicación: diciembre de 2016

**Problema conocido:**

* regla de notificación de Hello issuerid para AD FS no está en esta compilación. regla de notificación de Hello issuerid es necesaria si se están realizando una federación varios dominios con Azure Active Directory (Azure AD). Si utilizas Azure AD Connect toomanage local implementación de AD FS, actualizar toothis compilación quita la regla de notificación de issuerid existente de hello de la configuración de AD FS. Se puede solucionar el problema de hello mediante la adición de reglas de notificación de hello issuerid después de la actualización de la instalación Hola. Para obtener más información sobre cómo agregar hello issuerid de reglas de notificaciones, consulte el artículo toothis en [compatibilidad con varios dominios para federar con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problema corregido:**

* Si no se abre el puerto 9090 para la conexión saliente de hello, hello Azure AD Connect instalación o actualización se produce un error.

>[!NOTE]
>Esta versión no es toocustomers disponible a través de la característica de conectar actualización automática de hello Azure AD.

## <a name="113700"></a>1.1.370.0
Fecha de publicación: diciembre de 2016

**Problemas conocidos**:

* regla de notificación de Hello issuerid para AD FS no está en esta compilación. regla de notificación de Hello issuerid es necesaria si se están realizando una federación varios dominios con Azure AD. Si utilizas Azure AD Connect toomanage local implementación de AD FS, actualizar toothis compilación quita la regla de notificación de issuerid existente de hello de la configuración de AD FS. Se puede solucionar el problema de hello mediante la adición de reglas de notificación de hello issuerid después de la instalación o actualización. Para obtener más información sobre cómo agregar issuerid de reglas de notificaciones, consulte el artículo toothis en [compatibilidad con varios dominios para federar con Azure AD](active-directory-aadconnect-multiple-domains.md).
* Puerto 9090 debe estar abierto toocomplete saliente.

**Nuevas características:**

* Autenticación de paso a través (versión preliminar)

>[!NOTE]
>Esta versión no es toocustomers disponible a través de la característica de conectar actualización automática de hello Azure AD.

## <a name="113430"></a>1.1.343.0
Fecha de publicación: noviembre de 2016

**Problema conocido:**

* regla de notificación de Hello issuerid para AD FS no está en esta compilación. regla de notificación de Hello issuerid es necesaria si se están realizando una federación varios dominios con Azure AD. Si utilizas Azure AD Connect toomanage local implementación de AD FS, actualizar toothis compilación quita la regla de notificación de issuerid existente de hello de la configuración de AD FS. Se puede solucionar el problema de hello mediante la adición de reglas de notificación de hello issuerid después de la instalación o actualización. Para obtener más información sobre cómo agregar issuerid de reglas de notificaciones, consulte el artículo toothis en [compatibilidad con varios dominios para federar con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problemas corregidos:**

* A veces, Azure AD Connect no se puede instalar porque es una cuenta de servicio local cuya contraseña cumple con el nivel de Hola de complejidad especificado por la directiva de contraseñas de la organización de Hola de toocreate no se puede.
* Se corrigió un problema donde reglas de unión no se vuelven a evaluar cuando un objeto en el espacio del conector de hello simultáneamente está fuera de ámbito para uno, una regla y estén en el ámbito de otro. Esto puede ocurrir si tiene dos o más reglas de unión cuyas condiciones de unión son mutuamente excluyentes.
* Se ha corregido un problema por el que no se procesan las reglas de sincronización entrantes (desde Azure AD) que no contienen reglas de unión si tienen valores de prioridad inferiores que aquellas que sí que las contienen.

**Mejoras:**

* Se agregó compatibilidad para la instalación de Azure AD Connect en Windows Server 2016 estándar o superior.
* Se agregó compatibilidad para utilizar SQL Server 2016 como base de datos remota de Hola para Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Fecha de publicación: agosto de 2016

**Problemas corregidos:**

* Intervalo de toosync de cambios no surten efecto hasta que después Hola se complete el siguiente ciclo de sincronización.
* El Asistente de Azure AD Connect no acepta cuentas de Azure AD cuyo nombre de usuario comience con un guion bajo (\_).
* Asistente de Azure AD Connect se produce un error cuenta de Azure AD de hello tooauthenticate si la contraseña de la cuenta de hello contiene demasiados caracteres especiales. Mensaje de error "no se puede toovalidate credenciales. Se produjo un error inesperado" .
* Desinstalar el servidor de almacenamiento provisional deshabilita la sincronización de contraseña en el inquilino de Azure AD y hace que toofail de sincronización de contraseña con el servidor activo.
* Sincronización de contraseña se produce un error en casos poco comunes cuando no hay ningún hash de contraseña almacenado en usuario Hola.
* Cuando se habilita el servidor de Azure AD Connect para el modo provisional, la escritura diferida de contraseñas se deshabilita temporalmente.
* Asistente de Azure AD Connect no muestra la sincronización de contraseña real de Hola y la configuración de reescritura de contraseña cuando el servidor está en modo de almacenamiento provisional. Siempre se muestran como deshabilitadas.
* Sincronización de toopassword de cambios de configuración y la escritura diferida de contraseñas no se conservan por el Asistente de Azure AD Connect cuando el servidor está en modo de almacenamiento provisional.

**Mejoras:**

* Actualiza hello ADSyncSyncCycle inicio cmdlet tooindicate independientemente de si está toosuccessfully capaz de iniciar un nuevo ciclo de sincronización o no.
* Ciclo de sincronización de hello agregado ADSyncSyncCycle Stop cmdlet tooterminate y operación, que están actualmente en curso.
* Ciclo de sincronización de hello actualizada ADSyncScheduler Stop cmdlet tooterminate y operación, que están actualmente en curso.
* Al configurar [extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md) en Asistente de Azure AD Connect, ahora se puede seleccionar atributo hello Azure AD de tipo "Cadena de Teletexto".

## <a name="111890"></a>1.1.189.0
Fecha de publicación: junio de 2016

**Problemas corregidos y mejoras:**

* Azure AD Connect ahora puede instalarse en un servidor conforme a FIPS.
  * Para la sincronización de contraseñas, consulte [Sincronización de contraseñas y FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Se ha corregido un problema donde un nombre NetBIOS no se pudo resolver toohello FQDN Hola conector de Active Directory.

## <a name="111800"></a>1.1.180.0
Fecha de publicación: mayo de 2016

**Nuevas características:**

* Le advierte y ayuda a comprobar los dominios, si no lo hizo antes de ejecutar Azure AD Connect.
* Se ha agregado compatibilidad con [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Agrega compatibilidad con hello más reciente [nube de Microsoft Azure Government](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infraestructura con los nuevos requisitos a la dirección URL.

**Problemas corregidos y mejoras:**

* Toohello filtrado agregado Editor de reglas de sincronización toomake se toofind fácil reglas de sincronización.
* Mejora el rendimiento en la eliminación de un espacio de conector.
* Se corrigió un problema cuando Hola mismo objeto tanto se eliminó y se agregan en Hola misma serie (llamado delete/agregar).
* Una regla de sincronización deshabilitada ya no vuelve a habilitar objetos y atributos incluidos durante la actualización del esquema de directorio o una actualización.

## <a name="111300"></a>1.1.130.0
Fecha de publicación: abril de 2016

**Nuevas características:**

* Agrega compatibilidad para los atributos multivalor demasiado[extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md).
* Agrega compatibilidad para más variaciones de configuración para [la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) toobe considera apto para la actualización.
* Se han agregado algunos cmdlets para el [programador personalizado](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Fecha de publicación: marzo de 2016

**Problemas corregidos:**

* Nos aseguramos de que la instalación rápida no se pueda usar en Windows Server 2008 (versión preliminar 2) porque la sincronización de contraseñas no es compatible con este sistema operativo.
* La actualización desde DirSync con una configuración de filtro personalizada no funcionó como se esperaba.
* Al actualizar la versión más reciente de tooa y no hay ninguna configuración de toohello de cambios, no se debe programar una importación o sincronización completa.

## <a name="111100"></a>1.1.110.0
Fecha de publicación: febrero de 2016

**Problemas corregidos:**

* Actualización desde versiones anteriores no funciona si la instalación de hello no está en la carpeta de hello predeterminada C:\Program Files.
* Si instala y borrar **iniciar el proceso de sincronización de hello** al final de saludo del Asistente para instalación de hello, ejecutar el Asistente para instalación Hola una segunda vez no permitirán el programador de Hola.
* Hello programador no funciona según lo previsto en los servidores donde hello formato de fecha y hora de US-en no se utiliza. También bloqueará `Get-ADSyncScheduler` tooreturn correcta veces.
* Si instaló una versión anterior de Azure AD Connect con AD FS como Hola actualización y la opción de inicio de sesión, no se puede ejecutar a Asistente para la instalación de Hola de nuevo.

## <a name="111050"></a>1.1.105.0
Fecha de publicación: febrero de 2016

**Nuevas características:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) para los clientes de configuración rápida.
* Compatibilidad con Hola, administrador global mediante la autenticación multifactor Azure y Privileged Identity Management en el Asistente para la instalación de Hola.
  * Necesita tooallow su tooalso proxy permitir tráfico toohttps://secure.aadcdn.microsoftonline-p.com si utiliza la autenticación multifactor.
  * Necesita la lista de sitios de confianza de tooadd https://secure.aadcdn.microsoftonline-p.com tooyour para el trabajo de la autenticación multifactor tooproperly.
* Permite cambiar el método de inicio de sesión del usuario de hello tras la instalación inicial.
* Permitir [dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) en el Asistente para la instalación de Hola. Esto también permite conectar tooforests donde no todos los dominios están disponibles.
* [Programador](active-directory-aadconnectsync-feature-scheduler.md) se basa en el motor de sincronización de toohello.

**Características que se promocionan de la vista previa tooGA:**

* [Escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md)
* [Extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md)

**Nuevas características de la versión preliminar:**

* Hola nueva predeterminada ciclo de sincronización intervalo es de 30 minutos. Usa toobe tres horas para todas las versiones anteriores. Agrega compatibilidad con toochange hello [programador](active-directory-aadconnectsync-feature-scheduler.md) comportamiento.

**Problemas corregidos:**

* Hola Compruebe la página de dominios DNS siempre no reconoce los dominios de Hola.
* Solicita las credenciales de administrador de dominio al configurar AD FS.
* Hola local de cuentas de AD no son reconocidas por el Asistente para la instalación Hola si se encuentra en un dominio con un árbol DNS diferente que el dominio raíz de Hola.

## <a name="1091310"></a>1.0.9131.0
Fecha de publicación: diciembre de 2015

**Problemas corregidos:**

* La sincronización de contraseñas podría no funcionar al cambiar las contraseñas en Active Directory Domain Services (AD DS), pero funciona al establecer una contraseña.
* Cuando se tiene un servidor proxy, tooAzure autenticación AD podría producir un error durante la instalación, o si se cancela una actualización en la página de configuración de Hola.
* La actualización desde una versión anterior de Azure AD Connect con una instalación completa de una instancia de SQL Server produce errores si no es administrador del sistema de SQL Server (SA).
* Actualizar desde una versión anterior de Azure AD Connect con un servidor SQL remoto, muestra el error de "no se puede tooaccess Hola base de datos SQL de ADSync" Hola.

## <a name="1091250"></a>1.0.9125.0
Fecha de publicación: noviembre de 2015

**Nuevas características:**

* Puede volver a configurar la confianza de AD FS tooAzure AD.
* Puede actualizar el esquema de Active Directory de Hola y volver a generar reglas de sincronización.
* Puede deshabilitar una regla de sincronización.
* Puede definir "AuthoritativeNull" como un nuevo literal en una regla de sincronización.

**Nuevas características de la versión preliminar:**

* [Azure AD Connect Health para sincronización](../connect-health/active-directory-aadconnect-health-sync.md)
* Compatibilidad para sincronización de contraseñas de [Servicios de dominio de Azure AD](../active-directory-passwords-update-your-own-password.md) .

**Nuevo escenarios admitido:**

* Admite varias organizaciones de Exchange locales. Consulte [Implementaciones híbridas con varios bosques de Active Directory](https://technet.microsoft.com/library/jj873754.aspx) para más información.

**Problemas corregidos:**

* Problemas de sincronización de contraseñas:
  * Un objeto que se mueve desde el ámbito tooin fuera de ámbito no tendrán su contraseña sincronizada. Esto incluye tanto UO como el filtrado de atributos.
  * Al seleccionar un nuevo tooinclude de unidad organizativa sincronizada no requiere una sincronización de contraseñas total.
  * Cuando se habilita un usuario deshabilitado no sincronizar contraseñas de Hola.
  * cola de reintento de contraseña de Hello es infinito y se ha quitado Hola anterior límite de 5.000 toobe objetos retirado.
* No se puede tooconnect tooActive directorio con el nivel funcional del bosque de Windows Server 2016.
* Grupo de hello toochange no se puede que se usa para filtros de grupo tras la instalación inicial de Hola.
* Ya no se crea un nuevo perfil de usuario en servidor de Azure AD Connect Hola para todos los usuarios realizar un cambio de contraseña con reescritura de contraseña habilitada.
* No se puede toouse entero largo valores ámbitos sincronizados reglas.
* casilla de verificación de Hola "reescritura de dispositivos" permanece deshabilitado si hay controladores de dominio no accesible.

## <a name="1086670"></a>1.0.8667.0
Fecha de publicación: agosto de 2015

**Nuevas características:**

* Hola ahora es el Asistente para la instalación de Azure AD Connect localizado tooall idiomas de Windows Server.
* Se ha agregado compatibilidad con el desbloqueo de cuentas cuando se usa la administración de contraseñas de Azure AD.

**Problemas corregidos:**

* Asistente de instalación de Azure AD Connect se bloquea si otro usuario continúa la instalación en lugar de hello quien inicia por primera vez instalación Hola.
* Si una desinstalación anterior de Azure AD Connect no toouninstall sincronización de Azure AD Connect correctamente, no es posible tooreinstall.
* No se puede instalar Azure AD Connect con la instalación rápida si Hola usuario no tiene dominio de hello raíz del bosque de Hola o si se utiliza una versión distinta del inglés de Active Directory.
* Si no se puede resolver el FQDN de la cuenta de usuario de Active Directory de Hola Hola, se muestra un mensaje de error puede inducir a error "Esquema de error toocommit Hola".
* Si se cambia la cuenta de hello utilizada en hello conector de Active Directory fuera Asistente hello, Asistente Hola produce un error en las ejecuciones posteriores.
* Azure AD Connect a veces se produce un error de tooinstall en un controlador de dominio.
* No se puede habilitar y deshabilitar el "Modo provisional" si se han agregado atributos de extensión.
* Escritura diferida de contraseñas en algunas configuraciones se produce un error debido a una contraseña incorrecta en hello conector de Active Directory.
* No se puede actualizar la sincronización de directorios si se usa en el filtrado de atributos el nombre distintivo (DN).
* Uso excesivo de CPU al utilizar el restablecimiento de contraseña.

**Características de versión la preliminar eliminadas:**

* característica de vista previa de Hello [reescritura de usuarios](active-directory-aadconnect-feature-preview.md#user-writeback) se quita temporalmente en función de los comentarios de nuestros clientes de vista previa. Se agregará más tarde después de que se ha dirigido Hola proporcionada comentarios.

## <a name="1086410"></a>1.0.8641.0
Fecha de publicación: junio de 2015

**Versión inicial de Azure AD Connect.**

Ha cambiado el nombre de la sincronización de Azure AD tooAzure AD Connect.

**Nuevas características:**

* Instalación de la [configuración rápida](active-directory-aadconnect-get-started-express.md)
* Posibilidad de [configurar AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* Posibilidad de [actualizar desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Se ha introducido el [modo de ensayo](active-directory-aadconnectsync-operations.md#staging-mode)

**Nuevas características de la versión preliminar:**

* [Reescritura de usuarios](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Escritura diferida de grupos](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md)
* [Extensiones de directorio](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Fecha de publicación: mayo de 2015

**Nuevo requisito**

* Ahora, Azure AD Sync requiere Hola .NET Framework versión 4.5.1 toobe instalado.

**Problemas corregidos:**

* La escritura diferida de contraseñas de Azure AD produce errores de conectividad de Service Bus.

## <a name="104910413"></a>1.0.491.0413
Fecha de publicación: abril de 2015

**Problemas corregidos y mejoras:**

* Hola conector de Active Directory no procesa las eliminaciones correctamente si está habilitada la Papelera de reciclaje de Hola y hay varios dominios en el bosque de Hola.
* rendimiento de Hola de operaciones de importación se ha mejorado para hello conector Azure Active Directory.
* Cuando un grupo ha superado el límite de pertenencia de hello (de forma predeterminada, el límite de Hola se establece too50, 000 objetos), se ha eliminado el grupo de hello en Azure Active Directory. Con un nuevo comportamiento hello, no se elimina el grupo de hello, se produce un error y no se exportan los cambios de pertenencia.
* No se puede aprovisionar un nuevo objeto si una eliminación provisional con hello que mismo DN ya está presente en el espacio del conector de Hola.
* Algunos objetos se marcan para la sincronización durante una sincronización delta, aunque no hay ningún cambio registrado en el objeto de Hola.
* Forzar una sincronización de contraseñas, también quita lista de DC de hello preferido.
* CSExportAnalyzer tiene problemas con algunos estados de objetos.

**Nuevas características:**

* Una unión puede conectarse demasiado "cualquiera" tipo de objeto en hello MV.

## <a name="104850222"></a>1.0.485.0222
Fecha de publicación: febrero de 2015

**Mejoras:**

* Rendimiento de importación mejorada.

**Problemas corregidos:**

* Sincronización de contraseñas respeta el atributo cloudFiltered de Hola que usa filtrado de atributos. Los objetos filtrados ya no pertenecen al ámbito de la sincronización de contraseñas.
* En raras ocasiones donde topología Hola tenía muchos controladores de dominio, no funcionará la sincronización de contraseña.
* Se ha habilitado "Servidor detenido" al importar desde Hola conector de Azure AD después de la administración de dispositivos en Azure AD/Intune.
* La unión de entidades de seguridad externas (FSP) desde varios dominios del mismo bosque produce un error de unión ambigua.

## <a name="104751202"></a>1.0.475.1202
Fecha de publicación: diciembre de 2014

**Nuevas características:**

* Ahora es posible realizar la sincronización de contraseñas con filtrado basado en atributos. Para más información, consulte el artículo sobre la [sincronización de contraseñas con filtrado](active-directory-aadconnectsync-configure-filtering.md).
* atributo de msDS-ExternalDirectoryObjectID Hola se reescriben tooActive Directory. Esta característica agrega compatibilidad para las aplicaciones de Office 365. Usa OAuth2 tooaccess buzones de correo en línea y locales en una implementación híbrida de Exchange.

**Problemas de actualización corregidos:**

* Una versión más reciente del Ayudante para el inicio de sesión de hello está disponible en el servidor de Hola.
* Una ruta de acceso de instalación personalizada era tooinstall usa Azure AD Sync.
* Una actualización de Hola de bloques del criterio de unión personalizado no válido.

**Otras correcciones:**

* Plantillas de hello fijo para Office Pro Plus.
* Se han corregido los problemas de instalación ocasionados por nombres de usuario que comienzan con un guión.
* Fijo perdedora Hola valor sourceAnchor cuando se ejecuta el Asistente para la instalación de hello una segunda vez.
* Se ha corregido el seguimiento ETW para la sincronización de contraseñas.

## <a name="104701023"></a>1.0.470.1023
Fecha de publicación: octubre de 2014

**Nuevas características:**

* Sincronización de contraseñas procedentes de múltiples tooAzure de Active Directory AD en local.
* Idiomas de Windows Server de tooall de interfaz de usuario de instalación localizada.

**Actualización de AADSync 1.0 GA**

Si ya tiene Azure AD Sync instalado, hay un paso adicional que tootake en caso de que has cambiado cualquiera de las reglas de sincronización de out-of-box Hola. Después de haber actualizado la versión de toohello 1.0.470.1023, se duplican las reglas de sincronización de hello que ha modificado. Para cada regla de sincronización modificada, Hola siguientes:

1.  Localice la regla de sincronización de Hola se ha modificado y tome nota de los cambios de Hola.
* Eliminar regla de sincronización de Hola.
* Busque la nueva regla de sincronización de Hola que se crea mediante la sincronización de Azure AD y, a continuación, vuelva a aplicar los cambios de Hola.

**Permisos para hello cuenta de Active Directory**

Hola cuenta de Active Directory debe tener valores hash de contraseña de permisos adicionales toobe tooread capaz de Hola desde Active Directory. Hola permisos toogrant se denominan "Replicar cambios de directorio" y "Directorio de replicar todos los cambios." Ambos permisos son toobe requiere tooread capaz de hello los hash de contraseña.

## <a name="104190911"></a>1.0.419.0911
Fecha de publicación: septiembre de 2014

**Versión inicial de Azure AD Sync.**

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
