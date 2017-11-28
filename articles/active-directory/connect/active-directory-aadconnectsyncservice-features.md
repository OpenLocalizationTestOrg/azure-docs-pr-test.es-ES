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
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="20837-103">Características del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="20837-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="20837-104">característica de sincronización de Hola de Azure AD Connect tiene dos componentes:</span><span class="sxs-lookup"><span data-stu-id="20837-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="20837-105">componente de Hello local denominado **sincronización de Azure AD Connect**, también denominados **motor de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="20837-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="20837-106">servicio de Hola que residen en Azure AD también se denomina **servicio de sincronización de Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="20837-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="20837-107">Este tema explica cómo las características de hello después de hello **servicio de sincronización de Azure AD Connect** trabajo y cómo se pueden configurar mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20837-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="20837-108">Estas opciones se configuran por hello [Azure módulo Active Directory para Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="20837-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="20837-109">Descárguelo e instálelo por separado desde Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="20837-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="20837-110">cmdlets de Hola que se documentan en este tema se introdujeron en hello [el lanzamiento de marzo de 2016 (compilación 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="20837-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="20837-111">Si no tiene los cmdlets de hello documentados en este tema o no generan Hola igual como resultado, a continuación, asegúrese de que se ejecute hello última versión.</span><span class="sxs-lookup"><span data-stu-id="20837-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="20837-112">configuración de hello toosee en su directorio de Azure AD, ejecute `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="20837-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="20837-113">![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="20837-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="20837-114">Muchas de estas opciones solo se pueden cambiar mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="20837-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="20837-115">Hello siguientes opciones se pueden configurar mediante `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="20837-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="20837-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="20837-116">DirSyncFeature</span></span> | <span data-ttu-id="20837-117">Comentario</span><span class="sxs-lookup"><span data-stu-id="20837-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="20837-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="20837-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="20837-119">Permite objetos toojoin en userPrincipalName en dirección tooprimary SMTP de adición.</span><span class="sxs-lookup"><span data-stu-id="20837-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="20837-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="20837-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="20837-121">Permite atributo userPrincipalName de Hola de tooupdate de motor de hello sincronización administrados de licencia (no federados) a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="20837-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="20837-122">Después de habilitar una característica, no se puede volver a deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="20837-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="20837-123">Desde el 24 de agosto de 2016 Hola característica *duplicar resistencia de atributo* está habilitada de forma predeterminada para Azure nuevos directorios de AD.</span><span class="sxs-lookup"><span data-stu-id="20837-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="20837-124">Esta característica también se implantará y habilitará en directorios creados antes de esta fecha.</span><span class="sxs-lookup"><span data-stu-id="20837-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="20837-125">Recibirá una notificación por correo electrónico cuando el directorio es sobre tooget esta característica está habilitada.</span><span class="sxs-lookup"><span data-stu-id="20837-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="20837-126">Hello siguiente se configura, Azure AD Connect y no se puede modificar por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="20837-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="20837-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="20837-127">DirSyncFeature</span></span> | <span data-ttu-id="20837-128">Comentario</span><span class="sxs-lookup"><span data-stu-id="20837-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="20837-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="20837-129">DeviceWriteback</span></span> |[<span data-ttu-id="20837-130">Azure AD Connect: habilitación de la escritura diferida de dispositivos</span><span class="sxs-lookup"><span data-stu-id="20837-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="20837-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="20837-131">DirectoryExtensions</span></span> |[<span data-ttu-id="20837-132">Sincronización de Azure AD Connect: Extensiones de directorio</span><span class="sxs-lookup"><span data-stu-id="20837-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="20837-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="20837-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="20837-134">Permite un toobe de atributo en cuarentena cuando es un duplicado de otro objeto en lugar de un error de objeto completo de Hola durante la exportación.</span><span class="sxs-lookup"><span data-stu-id="20837-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="20837-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="20837-135">PasswordSync</span></span> |[<span data-ttu-id="20837-136">Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="20837-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="20837-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="20837-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="20837-138">Versión preliminar: reescritura de grupos</span><span class="sxs-lookup"><span data-stu-id="20837-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="20837-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="20837-139">UserWriteback</span></span> |<span data-ttu-id="20837-140">No se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="20837-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="20837-141">Resistencia de atributos duplicados</span><span class="sxs-lookup"><span data-stu-id="20837-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="20837-142">En lugar de un error tooprovision objetos que tienen un UPN duplicado / proxyAddresses, atributo duplicado Hola se "pone en cuarentena" y se asigna un valor temporal.</span><span class="sxs-lookup"><span data-stu-id="20837-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="20837-143">Una vez resuelto el conflicto de hello, Hola UPN es cambiar un valor adecuado toohello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="20837-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="20837-144">Para obtener más información, consulte [Sincronización de identidades y resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="20837-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="20837-145">Coincidencia parcial de UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="20837-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="20837-146">Cuando esta característica está habilitada, soft-match está habilitada para el UPN en suma toohello [dirección SMTP principal](https://support.microsoft.com/kb/2641663), que siempre está habilitada.</span><span class="sxs-lookup"><span data-stu-id="20837-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="20837-147">Soft-match es toomatch usado los usuarios existentes de la nube en Azure AD con usuarios locales.</span><span class="sxs-lookup"><span data-stu-id="20837-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="20837-148">Si necesita toomatch cuentas locales de AD con las cuentas existentes creadas en la nube de hello y no está usando Exchange Online, a continuación, esta característica es útil.</span><span class="sxs-lookup"><span data-stu-id="20837-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="20837-149">En este escenario, por lo general no tener un atributo de SMTP de motivo tooset hello en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="20837-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="20837-150">Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados.</span><span class="sxs-lookup"><span data-stu-id="20837-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="20837-151">Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20837-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="20837-152">Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20837-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="20837-153">Sincronización de las actualizaciones de userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="20837-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="20837-154">Históricamente, atributo de UserPrincipalName toohello actualizaciones mediante el servicio de sincronización de Hola desde local se ha bloqueado, a menos que ambas condiciones son verdaderas:</span><span class="sxs-lookup"><span data-stu-id="20837-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="20837-155">usuario de Hello administrado (no federados).</span><span class="sxs-lookup"><span data-stu-id="20837-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="20837-156">no se ha asignado una licencia al usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="20837-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="20837-157">Para obtener más información, consulte [usuario no coinciden con los nombres de Office 365, Azure o Intune Hola UPN local o Id. de inicio de sesión alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="20837-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="20837-158">Esta característica permite Hola sincronización motor tooupdate Hola userPrincipalName cuando es modificada en el local y utilizar la sincronización de contraseñas. Si utiliza la federación, no se admite esta característica.</span><span class="sxs-lookup"><span data-stu-id="20837-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="20837-159">Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados.</span><span class="sxs-lookup"><span data-stu-id="20837-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="20837-160">Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20837-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="20837-161">Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20837-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="20837-162">Después de habilitar esta característica, los valores existentes de userPrincipalName permanecerán tal cual.</span><span class="sxs-lookup"><span data-stu-id="20837-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="20837-163">En el próximo cambio de hello userPrincipalName atributo local, sincronización de diferencias normal de hello en los usuarios actualizará Hola UPN.</span><span class="sxs-lookup"><span data-stu-id="20837-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="20837-164">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="20837-164">See also</span></span>
* [<span data-ttu-id="20837-165">Sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="20837-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="20837-166">[Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="20837-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

