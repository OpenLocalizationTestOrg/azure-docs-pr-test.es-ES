---
title: Atributos sincronizados por Azure AD Connect | Microsoft Docs
description: Enumera los atributos que se sincronizan con Azure Active Directory.
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 1d935b73e1087d5ad858bdbee9af68dd1cf5cd1e
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="azure-ad-connect-sync-attributes-synchronized-to-azure-active-directory"></a>Azure AD Connect Sync: atributos sincronizados con Azure Active Directory
En este tema se enumeran los atributos que se sincronizan mediante la sincronización de Azure AD Connect.  
Los atributos se agrupan por la aplicación de Azure AD relacionada.

## <a name="attributes-to-synchronize"></a>Atributos que sincronizar
Una pregunta frecuente es *qué es la lista de atributos mínimos que sincronizar*. El método predeterminado y recomendado consiste en mantener los atributos predeterminados para poder crear una lista global de direcciones completa en la nube y obtener todas las características en cargas de trabajo de Office 365. En algunos casos, la organización no quiere que se sincronicen ciertos atributos en la nube porque contienen datos confidenciales o PII (información de identificación personal), como en el ejemplo siguiente:   
![Atributos incorrectos](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

En este caso, comience con la lista de atributos de este tema e identifique aquellos que podrían contener datos confidenciales o PII y que, por tanto, no se pueden sincronizar. Después, anule la selección de ellos durante la instalación con el [filtrado de atributos y aplicaciones de Azure AD](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Al anular la selección de atributos, debe tener cuidado y solo hacerlo con aquellos que sean imposibles de sincronizar. Anular la selección de otros atributos podría afectar negativamente a las características.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nombre del atributo | Usuario | Comentario |
| --- |:---:| --- |
| accountEnabled |X |Define si se habilita una cuenta. |
| cn |X | |
| DisplayName |X | |
| objectSID |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| pwdLastSet |X |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| sourceAnchor |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| usageLocation |X |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |

## <a name="exchange-online"></a>Exchange Online
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| assistant |X |X | | |
| altRecipient |X | | |Requiere la compilación 1.1.552.0 de Azure AD Connect o versiones posteriores. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| Descripción |X |X |X | |
| DisplayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |Este atributo no se consume actualmente para grupos. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Disponible en Azure AD Connect versión 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Este atributo no se consume actualmente por Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Este atributo no se consume actualmente por Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Este atributo no se consume actualmente por Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Este atributo no se consume actualmente por Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Este atributo no se consume actualmente por Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| Descripción |X |X |X | |
| DisplayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | |Exchange Online no usa actualmente este atributo. |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| URL |X |X | | |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |
| wWWHomePage |X |X | | |

## <a name="lync-online-subsequently-known-as-skype-for-business"></a>Lync Online (posteriormente se conoce como Skype Empresarial)
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| Descripción |X |X |X | |
| DisplayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| cn |X | |X |Nombre común o alias. Frecuentemente el prefijo del valor de [mail]. |
| DisplayName |X |X |X |Una cadena que representa el nombre que se muestra a menudo como el nombre descriptivo (nombre, apellido). |
| mail |X |X |X |Dirección de correo electrónico completa. |
| member | | |X | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X |Propiedad mecánica. Usado por Azure AD. Contiene todas las direcciones de correo electrónico secundarias para el usuario. |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. |
| securityEnabled | | |X |Deriva de groupType. |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |Este UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |

## <a name="intune"></a>Intune
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| Descripción |X |X |X | |
| DisplayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| Descripción |X |X |X | |
| DisplayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| título |X |X | | |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |

## <a name="3rd-party-applications"></a>Aplicaciones de terceros
Este grupo es un conjunto de atributos que se usan como atributos mínimos necesarios para una carga de trabajo o aplicación genérica. Se puede emplear para cargas de trabajo que no figuren en otra sección o para una aplicación que no sea de Microsoft. Se usa explícitamente para lo siguiente:

* Yammer (solo se consume User)
* [Escenarios híbridos de colaboración entre organizaciones negocio a negocio (B2B) ofrecidos por recursos como SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Este grupo es un conjunto de atributos que se pueden usar si no se emplea el directorio de Azure AD para admitir Office 365, Dynamics o Intune. Tiene un pequeño conjunto de atributos principales.

| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| cn |X | |X | |
| DisplayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |Propiedad mecánica. Identificador de usuario de AD usado para mantener la sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Usada para saber cuándo invalidar tokens ya emitidos. Usada por sincronización de contraseñas y federación. |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Identificador inmutable para mantener la relación entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. El país del usuario. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es el identificador de inicio de sesión para el usuario. Frecuentemente el mismo que el valor [mail]. |

## <a name="windows-10"></a>Windows 10
Los equipos (dispositivos) Windows 10 unidos a un dominio sincronizarán algunos atributos con Azure AD. Para obtener más información sobre los escenarios, vea [Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10](../active-directory-azureadjoin-devices-group-policy.md). Estos atributos siempre se sincronizarán y Windows 10 no aparecerá como una aplicación de la que puede anular la selección. Un equipo unido a un dominio de Windows 10 se identifica por tener el atributo userCertificate rellenado.

| Nombre del atributo | Dispositivo | Comentario |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Valor codificado de forma rígida para equipos unidos al dominio. |
| DisplayName |X | |
| ms-DS-CreatorSID |X |También se denomina registeredOwnerReference. |
| objectGUID |X |También se denomina deviceID. |
| objectSID |X |También se denomina onPremisesSecurityIdentifier. |
| operatingSystem |X |También se denomina deviceOSType. |
| operatingSystemVersion |X |También se denomina deviceOSVersion. |
| userCertificate |X | |

Estos atributos de **User** se incluyen además de las otras aplicaciones que haya seleccionado.  

| Nombre del atributo | Usuario | Comentario |
| --- |:---:| --- |
| domainFQDN |X |También se denomina dnsDomainName. Por ejemplo, contoso.com. |
| domainNetBios |X |También se denomina netBiosName. Por ejemplo, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Reescritura híbrida de Exchange
Estos atributos se reescriben desde Azure AD en Active Directory local cuando se elige habilitar la **implementación híbrida de Exchange**. Dependiendo de la versión de Exchange, puede que se sincronicen menos atributos.

| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Se deriva de cloudAnchor en Azure AD. Este atributo es nuevo en Exchange 2016 y en AD de Windows Server 2016. |
| msExchArchiveStatus |X | | |Archivo en línea: permite a los clientes archivar el correo electrónico. |
| msExchBlockedSendersHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchSafeRecipientsHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchSafeSendersHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchUCVoiceMailSettings |X | | |Habilitar mensajería unificada (UM) - correo de voz en línea: usado para la integración de Microsoft Lync Server para indicar a Lync Server local que el usuario tiene el correo de voz en los servicios en línea. |
| msExchUserHoldPolicies |X | | |Retención por juicio: permite que los servicios en la nube determinen qué usuarios están bajo retención por juicio. |
| proxyAddresses |X |X |X |Solo se inserta la dirección x500 de Exchange Online. |
| publicDelegates |X | | |Permite conceder derechos SendOnBehalfTo a un buzón de Exchange Online para los usuarios con buzones de Exchange locales. Requiere la compilación 1.1.552.0 de Azure AD Connect o versiones posteriores. |

## <a name="exchange-mail-public-folder"></a>Carpeta pública de correo de Exchange
Estos atributos se sincronizan desde Active Directory local en Azure AD cuando se elige habilitar la **carpeta pública de correo de Exchange**.

| Nombre del atributo | PublicFolder | Comentario |
| --- | :---:| --- |
| DisplayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Escritura diferida de dispositivos
Los objetos de dispositivo se crean en Active Directory. Pueden ser dispositivos unidos a Azure AD o equipos Windows 10 unidos a un dominio.

| Nombre del atributo | Dispositivo | Comentario |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| DisplayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Solo con el esquema de Windows Server 2016 AD |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Notas
* Cuando se usa un identificador alternativo, el atributo local userPrincipalName se sincronizará con el de Azure AD onPremisesUserPrincipalName. El atributo de identificador alternativo, por ejemplo, mail, se sincronizará con el de Azure AD userPrincipalName.
* En la lista anterior, el tipo de objeto **User** también se aplica al tipo de objeto **iNetOrgPerson**.

## <a name="next-steps"></a>pasos siguientes
Obtenga más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) .

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
