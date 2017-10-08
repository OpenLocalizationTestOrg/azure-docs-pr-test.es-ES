---
title: "características y configuración de servicio aaaAzure AD Connect sync | Documentos de Microsoft"
description: "Describe las características del servicio de sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Características del servicio de sincronización de Azure AD Connect
característica de sincronización de Hola de Azure AD Connect tiene dos componentes:

* componente de Hello local denominado **sincronización de Azure AD Connect**, también denominados **motor de sincronización**.
* servicio de Hola que residen en Azure AD también se denomina **servicio de sincronización de Azure AD Connect**

Este tema explica cómo las características de hello después de hello **servicio de sincronización de Azure AD Connect** trabajo y cómo se pueden configurar mediante Windows PowerShell.

Estas opciones se configuran por hello [Azure módulo Active Directory para Windows PowerShell](http://aka.ms/aadposh). Descárguelo e instálelo por separado desde Azure AD Connect. cmdlets de Hola que se documentan en este tema se introdujeron en hello [el lanzamiento de marzo de 2016 (compilación 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Si no tiene los cmdlets de hello documentados en este tema o no generan Hola igual como resultado, a continuación, asegúrese de que se ejecute hello última versión.

configuración de hello toosee en su directorio de Azure AD, ejecute `Get-MsolDirSyncFeatures`.  
![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Muchas de estas opciones solo se pueden cambiar mediante Azure AD Connect.

Hello siguientes opciones se pueden configurar mediante `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentario |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Permite objetos toojoin en userPrincipalName en dirección tooprimary SMTP de adición. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Permite atributo userPrincipalName de Hola de tooupdate de motor de hello sincronización administrados de licencia (no federados) a los usuarios. |

Después de habilitar una característica, no se puede volver a deshabilitar.

> [!NOTE]
> Desde el 24 de agosto de 2016 Hola característica *duplicar resistencia de atributo* está habilitada de forma predeterminada para Azure nuevos directorios de AD. Esta característica también se implantará y habilitará en directorios creados antes de esta fecha. Recibirá una notificación por correo electrónico cuando el directorio es sobre tooget esta característica está habilitada.
> 
> 

Hello siguiente se configura, Azure AD Connect y no se puede modificar por `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentario |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: habilitación de la escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Sincronización de Azure AD Connect: Extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Permite un toobe de atributo en cuarentena cuando es un duplicado de otro objeto en lugar de un error de objeto completo de Hola durante la exportación. |
| PasswordSync |[Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Versión preliminar: reescritura de grupos](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |No se admite actualmente. |

## <a name="duplicate-attribute-resiliency"></a>Resistencia de atributos duplicados
En lugar de un error tooprovision objetos que tienen un UPN duplicado / proxyAddresses, atributo duplicado Hola se "pone en cuarentena" y se asigna un valor temporal. Una vez resuelto el conflicto de hello, Hola UPN es cambiar un valor adecuado toohello automáticamente. Para obtener más información, consulte [Sincronización de identidades y resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Coincidencia parcial de UserPrincipalName
Cuando esta característica está habilitada, soft-match está habilitada para el UPN en suma toohello [dirección SMTP principal](https://support.microsoft.com/kb/2641663), que siempre está habilitada. Soft-match es toomatch usado los usuarios existentes de la nube en Azure AD con usuarios locales.

Si necesita toomatch cuentas locales de AD con las cuentas existentes creadas en la nube de hello y no está usando Exchange Online, a continuación, esta característica es útil. En este escenario, por lo general no tener un atributo de SMTP de motivo tooset hello en la nube de Hola.

Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados. Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Sincronización de las actualizaciones de userPrincipalName
Históricamente, atributo de UserPrincipalName toohello actualizaciones mediante el servicio de sincronización de Hola desde local se ha bloqueado, a menos que ambas condiciones son verdaderas:

* usuario de Hello administrado (no federados).
* no se ha asignado una licencia al usuario Hola.

Para obtener más información, consulte [usuario no coinciden con los nombres de Office 365, Azure o Intune Hola UPN local o Id. de inicio de sesión alternativo](https://support.microsoft.com/kb/2523192).

Esta característica permite Hola sincronización motor tooupdate Hola userPrincipalName cuando es modificada en el local y utilizar la sincronización de contraseñas. Si utiliza la federación, no se admite esta característica.

Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados. Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Después de habilitar esta característica, los valores existentes de userPrincipalName permanecerán tal cual. En el próximo cambio de hello userPrincipalName atributo local, sincronización de diferencias normal de hello en los usuarios actualizará Hola UPN.  

## <a name="see-also"></a>Otras referencias
* [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

