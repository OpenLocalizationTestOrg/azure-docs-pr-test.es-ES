---
title: "Características y configuración del servicio de sincronización de Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="3a27d-103">Características del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3a27d-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="3a27d-104">La característica de sincronización de Azure AD Connect tiene dos componentes:</span><span class="sxs-lookup"><span data-stu-id="3a27d-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="3a27d-105">El componente local denominado **sincronización de Azure AD Connect**, también conocido como **motor de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="3a27d-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="3a27d-106">El servicio que se encuentra en Azure AD, también conocido como **servicio de sincronización de Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="3a27d-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="3a27d-107">En este tema se explica cómo funcionan las siguientes características del **servicio de sincronización de Azure AD Connect** y cómo puede configurarlas mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a27d-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="3a27d-108">Estas opciones se configuran mediante el [módulo Azure Active Directory para Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="3a27d-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="3a27d-109">Descárguelo e instálelo por separado desde Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3a27d-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="3a27d-110">Los cmdlets descritos en este tema se introdujeron con la [versión de marzo de 2016 (compilación 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="3a27d-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="3a27d-111">Si no tiene los cmdlets que se documentan en este tema o estos no generan el mismo resultado, asegúrese de que ejecuta la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="3a27d-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="3a27d-112">Para ver la configuración en el directorio de Azure AD, ejecute `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="3a27d-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="3a27d-113">![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="3a27d-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="3a27d-114">Muchas de estas opciones solo se pueden cambiar mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3a27d-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="3a27d-115">Se pueden configurar las siguientes opciones en `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3a27d-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3a27d-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3a27d-116">DirSyncFeature</span></span> | <span data-ttu-id="3a27d-117">Comentario</span><span class="sxs-lookup"><span data-stu-id="3a27d-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="3a27d-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="3a27d-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="3a27d-119">Permite que los objetos se unan a userPrincipalName además de la dirección SMTP principal.</span><span class="sxs-lookup"><span data-stu-id="3a27d-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="3a27d-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="3a27d-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="3a27d-121">Permite que el motor de sincronización actualice el atributo userPrincipalName para los usuarios administrados y con licencia (no federados).</span><span class="sxs-lookup"><span data-stu-id="3a27d-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="3a27d-122">Después de habilitar una característica, no se puede volver a deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="3a27d-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="3a27d-123">Desde el 24 de agosto de 2016, la característica *Resistencia de atributos duplicados* está habilitada de forma predeterminada para nuevos directorios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a27d-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="3a27d-124">Esta característica también se implantará y habilitará en directorios creados antes de esta fecha.</span><span class="sxs-lookup"><span data-stu-id="3a27d-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="3a27d-125">Recibirá una notificación por correo electrónico cuando el directorio esté próximo a habilitar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3a27d-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="3a27d-126">Las siguientes opciones se configuran mediante Azure AD Connect y no se pueden modificar por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3a27d-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3a27d-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3a27d-127">DirSyncFeature</span></span> | <span data-ttu-id="3a27d-128">Comentario</span><span class="sxs-lookup"><span data-stu-id="3a27d-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="3a27d-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="3a27d-129">DeviceWriteback</span></span> |[<span data-ttu-id="3a27d-130">Azure AD Connect: habilitación de la escritura diferida de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3a27d-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="3a27d-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="3a27d-131">DirectoryExtensions</span></span> |[<span data-ttu-id="3a27d-132">Sincronización de Azure AD Connect: Extensiones de directorio</span><span class="sxs-lookup"><span data-stu-id="3a27d-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="3a27d-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="3a27d-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="3a27d-134">Permite poner un atributo en cuarentena si es un duplicado de otro objeto en lugar de consignar un error en todo el objeto durante la exportación.</span><span class="sxs-lookup"><span data-stu-id="3a27d-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="3a27d-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="3a27d-135">PasswordSync</span></span> |[<span data-ttu-id="3a27d-136">Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3a27d-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="3a27d-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="3a27d-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="3a27d-138">Versión preliminar: reescritura de grupos</span><span class="sxs-lookup"><span data-stu-id="3a27d-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="3a27d-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="3a27d-139">UserWriteback</span></span> |<span data-ttu-id="3a27d-140">No se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="3a27d-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="3a27d-141">Resistencia de atributos duplicados</span><span class="sxs-lookup"><span data-stu-id="3a27d-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="3a27d-142">En lugar de no aprovisionar objetos con atributos UPN/proxyAddresses duplicados, el atributo duplicado se "pone en cuarentena" y se le asigna un valor temporal.</span><span class="sxs-lookup"><span data-stu-id="3a27d-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="3a27d-143">Cuando se resuelve el conflicto, el UPN temporal se cambia por el valor correcto automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3a27d-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="3a27d-144">Para obtener más información, consulte [Sincronización de identidades y resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="3a27d-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="3a27d-145">Coincidencia parcial de UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3a27d-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="3a27d-146">Cuando esta característica está habilitada, se activa la coincidencia parcial en UPN, así como la [dirección SMTP principal](https://support.microsoft.com/kb/2641663), que siempre está habilitada.</span><span class="sxs-lookup"><span data-stu-id="3a27d-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="3a27d-147">La coincidencia parcial se utiliza para hacer coincidir los usuarios de Azure AD en la nube con los locales.</span><span class="sxs-lookup"><span data-stu-id="3a27d-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="3a27d-148">Si necesita que coincidan las cuentas de AD locales con las cuentas existentes creadas en la nube y no está utilizando Exchange Online, esta característica resulta útil.</span><span class="sxs-lookup"><span data-stu-id="3a27d-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="3a27d-149">En este escenario, normalmente no tiene una razón para establecer el atributo de SMTP en la nube.</span><span class="sxs-lookup"><span data-stu-id="3a27d-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="3a27d-150">Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados.</span><span class="sxs-lookup"><span data-stu-id="3a27d-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3a27d-151">Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a27d-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="3a27d-152">Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a27d-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="3a27d-153">Sincronización de las actualizaciones de userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3a27d-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="3a27d-154">Históricamente, las actualizaciones para el atributo UserPrincipalName con el servicio de sincronización desde una instancia local han estado bloqueadas, a menos que se cumplieran las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="3a27d-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="3a27d-155">El usuario está administrado (no federado).</span><span class="sxs-lookup"><span data-stu-id="3a27d-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="3a27d-156">Al usuario no se le ha asignado una licencia.</span><span class="sxs-lookup"><span data-stu-id="3a27d-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="3a27d-157">Para obtener más información, consulte [Nombres de usuario en Office 365, Azure o Intune no coinciden con el UPN local o el identificador de inicio de sesión alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="3a27d-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="3a27d-158">Esta característica permite al motor de sincronización actualizar el valor de userPrincipalName cuando se modifica de manera local y se usa la sincronización de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="3a27d-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="3a27d-159">Si utiliza la federación, no se admite esta característica.</span><span class="sxs-lookup"><span data-stu-id="3a27d-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="3a27d-160">Esta característica está activa de forma predeterminada para los directorios de Azure AD recién creados.</span><span class="sxs-lookup"><span data-stu-id="3a27d-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3a27d-161">Puede ver si esta característica está habilitada en su caso ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a27d-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="3a27d-162">Si esta característica no está habilitada para el directorio de Azure AD, puede habilitarla ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a27d-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="3a27d-163">Después de habilitar esta característica, los valores existentes de userPrincipalName permanecerán tal cual.</span><span class="sxs-lookup"><span data-stu-id="3a27d-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="3a27d-164">En el próximo cambio del atributo userPrincipalName en la instancia local, la sincronización diferencial normal de los usuarios actualizará el UPN.</span><span class="sxs-lookup"><span data-stu-id="3a27d-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3a27d-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3a27d-165">See also</span></span>
* [<span data-ttu-id="3a27d-166">Sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3a27d-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="3a27d-167">[Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3a27d-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

