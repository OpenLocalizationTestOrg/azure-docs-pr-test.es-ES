---
title: Atributos sincronizados por Azure AD Connect | Microsoft Docs
description: Listas de hello atributos sincronizan tooAzure Active Directory.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Azure AD Connect sync: atributos sincronizados tooAzure Active Directory
En este tema se enumera los atributos de Hola que se sincronizan mediante la sincronización de Azure AD Connect.  
Hello atributos agrupados por hello relacionados con la aplicación de Azure AD.

## <a name="attributes-toosynchronize"></a>Atributos toosynchronize
Una pregunta frecuente es *¿qué es la lista de Hola de atributos mínimos toosynchronize*. valor predeterminado de Hola y enfoque recomendado es atributos predeterminados de tookeep Hola por lo que se puede construir una GAL completa (lista Global de direcciones) en hello en la nube y tooget todas las características de las cargas de trabajo de Office 365. En algunos casos, hay algunos atributos que su organización no desea toohello sincronizada en la nube ya contienen estos atributos confidenciales o datos PII (información de identificación personal), al igual que en este ejemplo:  
![Atributos incorrectos](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

En este caso, comience con la lista de Hola de atributos en este tema e identificar los atributos que contengan confidencial o datos PII y no se puede sincronizar. Después, anule la selección de ellos durante la instalación con el [filtrado de atributos y aplicaciones de Azure AD](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Al anular la selección de atributos, debe tener cuidado y solo anule la selección esos toosynchronize absolutamente no son posibles atributos. Anular la selección de otros atributos podría afectar negativamente a las características.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nombre del atributo | Usuario | Comentario |
| --- |:---:| --- |
| accountEnabled |X |Define si se habilita una cuenta. |
| cn |X | |
| DisplayName |X | |
| objectSID |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| pwdLastSet |X |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| sourceAnchor |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| usageLocation |X |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |

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
| description |X |X |X | |
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
| mangedBy | | |X | |
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
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |
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
| description |X |X |X | |
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
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
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
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| description |X |X |X | |
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
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| cn |X | |X |Nombre común o alias. Con mayor frecuencia prefijo de Hola de valor [mail]. |
| DisplayName |X |X |X |Una cadena que representa el nombre de hello suele mostrado como nombre descriptivo de hello (nombre apellido). |
| mail |X |X |X |Dirección de correo electrónico completa. |
| member | | |X | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X |Propiedad mecánica. Usado por Azure AD. Contiene todas las direcciones de correo electrónico secundarias para el usuario de Hola. |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. |
| securityEnabled | | |X |Deriva de groupType. |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |Este UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |

## <a name="intune"></a>Intune
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| DisplayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define si se habilita una cuenta. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| DisplayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| securityEnabled | | |X |Deriva de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| título |X |X | | |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |

## <a name="3rd-party-applications"></a>Aplicaciones de terceros
Este grupo es un conjunto de atributos que se utilizan como Hola atributos mínimos necesarios para una carga de trabajo genérica o una aplicación. Se puede emplear para cargas de trabajo que no figuren en otra sección o para una aplicación que no sea de Microsoft. Explícitamente se usa para siguiente hello:

* Yammer (solo se consume User)
* [Escenarios híbridos de colaboración entre organizaciones negocio a negocio (B2B) ofrecidos por recursos como SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Este grupo es un conjunto de atributos que puede utilizarse si no es el directorio de Azure AD de hello usa toosupport Office 365, Dynamics o Intune. Tiene un pequeño conjunto de atributos principales.

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
| objectSID |X | | |Propiedad mecánica. Identificador de usuario de AD usa toomaintain sincronización entre Azure AD y AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Propiedad mecánica. Tooknow usado cuando tooinvalidate ya los tokens emitidos. Usada por sincronización de contraseñas y federación. |
| sn |X |X | | |
| sourceAnchor |X |X |X |Propiedad mecánica. Relación de toomaintain identificador inmutable entre ADDS y Azure AD. |
| usageLocation |X | | |Propiedad mecánica. país del usuario de Hola. Se usa para la asignación de licencias. |
| userPrincipalName |X | | |UPN es Hola Id. de inicio de sesión de usuario de Hola. Con mayor frecuencia Hola igual que el valor [mail]. |

## <a name="windows-10"></a>Windows 10
Un computer(device) Unidos a un dominio de Windows 10 sincroniza algunos tooAzure atributos AD. Para obtener más información sobre los escenarios de hello, consulte [conectar dispositivos Unidos a dominio tooAzure AD para Windows 10 experimenta](../active-directory-azureadjoin-devices-group-policy.md). Estos atributos siempre se sincronizarán y Windows 10 no aparecerá como una aplicación de la que puede anular la selección. Un equipo unido a un dominio de Windows 10 se identifica por tener Hola atributo userCertificate rellena.

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

Estos atributos para **usuario** es además toohello otras aplicaciones que ha seleccionado.  

| Nombre del atributo | Usuario | Comentario |
| --- |:---:| --- |
| domainFQDN |X |También se denomina dnsDomainName. Por ejemplo, contoso.com. |
| domainNetBios |X |También se denomina netBiosName. Por ejemplo, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Reescritura híbrida de Exchange
Estos atributos se reescriben desde Azure AD tooon-local de Active Directory cuando se selecciona tooenable **implementación híbrida de Exchange**. Dependiendo de la versión de Exchange, puede que se sincronicen menos atributos.

| Nombre del atributo | Usuario | Contacto | Grupo | Comentario |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Se deriva de cloudAnchor en Azure AD. Este atributo es nuevo en Exchange 2016 y en AD de Windows Server 2016. |
| msExchArchiveStatus |X | | |Archivo en línea: Habilita tooarchive de correo electrónico de los clientes. |
| msExchBlockedSendersHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchSafeRecipientsHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchSafeSendersHash |X | | |Filtrado: reescribe los datos de remitentes seguros y bloqueados en línea y el filtrado de local de los clientes. |
| msExchUCVoiceMailSettings |X | | |Habilitar la mensajería unificada (UM) - correo de voz en línea: usa Microsoft Lync Server integración tooindicate tooLync servidor local que el usuario hello tiene correo de voz en los servicios en línea. |
| msExchUserHoldPolicies |X | | |Suspensión de juicio: Permite toodetermine de servicios de nube que los usuarios están bajo juicio mantenga. |
| proxyAddresses |X |X |X |Solo hello x500 dirección de Exchange Online se inserta. |
| publicDelegates |X | | |Permite que un toobe de buzón de Exchange Online concedido SendOnBehalfTo derechos toousers con buzón de Exchange local. Requiere la compilación 1.1.552.0 de Azure AD Connect o versiones posteriores. |

## <a name="exchange-mail-public-folder"></a>Carpeta pública de correo de Exchange
Estos atributos se sincronizan desde tooAzure de Active Directory local AD cuando selecciona tooenable **carpetas públicas de correo electrónico de Exchange**.

| Nombre del atributo | PublicFolder | Comentario |
| --- | :---:| --- |
| DisplayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Escritura diferida de dispositivos
Los objetos de dispositivo se crean en Active Directory. Estos objetos pueden ser dispositivos Unidos tooAzure AD o equipos unidos a un dominio de Windows 10.

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
* Al usar un Id. alternativo, hello locales atributo userPrincipalName se sincroniza con onPremisesUserPrincipalName de atributo de hello Azure AD. Hola atributo de Id. alternativo, por ejemplo correo electrónico, se sincroniza con el atributo userPrincipalName de hello Azure AD.
* En las listas de hello anteriores, tipo de objeto de Hola **usuario** también se aplica el tipo de objeto de toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
