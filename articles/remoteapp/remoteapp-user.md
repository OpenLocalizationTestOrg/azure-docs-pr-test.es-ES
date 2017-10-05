---
title: "Adición de un usuario a la colección de Azure RemoteApp | Microsoft Docs"
description: "Obtenga información acerca de cómo agregar usuarios a la aplicación de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="bfbeb-103">Agregar usuarios a la aplicación de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bfbeb-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bfbeb-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bfbeb-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="bfbeb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bfbeb-106">Para que los usuarios puedan ver y usar las aplicaciones en Azure RemoteApp, debe concederles acceso a la colección.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="bfbeb-107">Esta es la parte fácil: en la pestaña **Acceso de usuario** , escriba la información de cuenta del usuario y, a continuación, haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="bfbeb-108">¿Qué información de cuenta necesita?</span><span class="sxs-lookup"><span data-stu-id="bfbeb-108">What account information do you need?</span></span> <span data-ttu-id="bfbeb-109">Depende del tipo de colección que haya creado (en nube o híbrida) y si está usando Office 365 ProPlus en esa colección.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="bfbeb-110">Identidades de usuario admitido</span><span class="sxs-lookup"><span data-stu-id="bfbeb-110">Supported user identities</span></span>
<span data-ttu-id="bfbeb-111">Los distintos tipos de colección (nube frente a híbrida) admiten el uso de distintas identidades de usuario para el acceso a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="bfbeb-112">Para una colección híbrida de RemoteApp, tendrá que configurar una infraestructura de dominio de Active Directory local y un inquilino de Azure Active Directory con integración de directorios (e inicio de sesión único opcional).</span><span class="sxs-lookup"><span data-stu-id="bfbeb-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="bfbeb-113">Además, deberá crear algunos objetos de Active Directory en el directorio local.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="bfbeb-114">Para una colección de nube de RemoteApp, a cualquier usuario con Azure Active Directory que admita identidades se le puede conceder acceso de usuario a RemoteApp para incluir cuentas Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="bfbeb-115">Consulte la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-115">See the table below.</span></span>

<span data-ttu-id="bfbeb-116">Los usuarios de Office 365 son usuarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="bfbeb-117">Si tienen cuentas de colección híbrida con sincronización de directorios de Azure Active Directory, se les puede conceder acceso de usuario en una implementación híbrida de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="bfbeb-118">Puede usar esta tabla como referencia rápida para saber qué identidad se admite en la colección y cuáles son los requisitos de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="bfbeb-119">Cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="bfbeb-119">User accounts</span></span> | <span data-ttu-id="bfbeb-120">Nube</span><span class="sxs-lookup"><span data-stu-id="bfbeb-120">Cloud</span></span> | <span data-ttu-id="bfbeb-121">Híbrida</span><span class="sxs-lookup"><span data-stu-id="bfbeb-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfbeb-122">Cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="bfbeb-122">Microsoft Account</span></span> |<span data-ttu-id="bfbeb-123">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-123">Yes</span></span> |<span data-ttu-id="bfbeb-124">No</span><span class="sxs-lookup"><span data-stu-id="bfbeb-124">No</span></span> |
| <span data-ttu-id="bfbeb-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="bfbeb-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="bfbeb-126">Solo nube de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfbeb-126">Azure AD cloud only</span></span> |<span data-ttu-id="bfbeb-127">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-127">Yes</span></span> |<span data-ttu-id="bfbeb-128">No</span><span class="sxs-lookup"><span data-stu-id="bfbeb-128">No</span></span> |
| <span data-ttu-id="bfbeb-129">ADsync con sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="bfbeb-129">ADsync with password sync</span></span> |<span data-ttu-id="bfbeb-130">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-130">Yes</span></span> |<span data-ttu-id="bfbeb-131">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-131">Yes</span></span> |
| <span data-ttu-id="bfbeb-132">ADsync sin sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="bfbeb-132">ADsync without password sync</span></span> |<span data-ttu-id="bfbeb-133">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-133">Yes</span></span> |<span data-ttu-id="bfbeb-134">No</span><span class="sxs-lookup"><span data-stu-id="bfbeb-134">No</span></span> |
| <span data-ttu-id="bfbeb-135">ADsync con AD FS</span><span class="sxs-lookup"><span data-stu-id="bfbeb-135">ADsync with AD FS</span></span> |<span data-ttu-id="bfbeb-136">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-136">Yes</span></span> |<span data-ttu-id="bfbeb-137">yes</span><span class="sxs-lookup"><span data-stu-id="bfbeb-137">Yes</span></span> |
| <span data-ttu-id="bfbeb-138">[Proveedores de identidades de terceros compatibles con Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por ejemplo, Ping)</span><span class="sxs-lookup"><span data-stu-id="bfbeb-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="bfbeb-139">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-139">Yes</span></span> |<span data-ttu-id="bfbeb-140">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-140">Yes</span></span> |
| <span data-ttu-id="bfbeb-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bfbeb-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="bfbeb-142">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-142">Yes</span></span> |<span data-ttu-id="bfbeb-143">Sí</span><span class="sxs-lookup"><span data-stu-id="bfbeb-143">Yes</span></span> |

<span data-ttu-id="bfbeb-144">Consulte [más información](remoteapp-ad.md) sobre cómo configurar Active Directory para RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="bfbeb-145">Los usuarios de Azure Active Directory deben proceder del inquilino asociado a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="bfbeb-146">(Puede ver y modificar su suscripción en la pestaña **Configuración** del portal.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="bfbeb-147">Consulte [Cambio del inquilino de Azure Active Directory que usa RemoteApp](remoteapp-changetenant.md) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="bfbeb-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="bfbeb-148">Información de la cuenta de usuario de Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="bfbeb-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="bfbeb-149">Si usa la imagen de plantilla de Office 365 ProPlus en su colección *o* si creó una imagen personalizada que usa Office 365, solo puede agregar usuarios de Azure Active Directory que tengan suscripciones de Office 365 para el dominio predeterminado de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="bfbeb-150">Consulte [Uso de Office 365 con RemoteApp de Azure](remoteapp-o365.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bfbeb-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

