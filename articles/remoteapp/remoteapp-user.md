---
title: "una colección de Azure RemoteApp de usuario tooyour aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd usuarios tooyour colección RemoteApp de Azure"
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
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="e237f-103">¿Cómo tooadd una colección de Azure RemoteApp tooyour de usuario</span><span class="sxs-lookup"><span data-stu-id="e237f-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e237f-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="e237f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e237f-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e237f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e237f-106">Antes de que los usuarios pueden ver y usar las aplicaciones de Azure RemoteApp, tendrá toogrant acceso tooyour colección.</span><span class="sxs-lookup"><span data-stu-id="e237f-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="e237f-107">Esto forma parte fácil hello: en hello **acceso de usuario** pestaña, escriba la información de la cuenta de hello para el usuario de Hola y, a continuación, haga clic en la casilla de verificación Hola.</span><span class="sxs-lookup"><span data-stu-id="e237f-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="e237f-108">¿Qué información de cuenta necesita?</span><span class="sxs-lookup"><span data-stu-id="e237f-108">What account information do you need?</span></span> <span data-ttu-id="e237f-109">Que depende Hola tipo de colección que ha creado (en la nube o híbridas) y si utilizas Office 365 ProPlus en esa colección.</span><span class="sxs-lookup"><span data-stu-id="e237f-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="e237f-110">Identidades de usuario admitido</span><span class="sxs-lookup"><span data-stu-id="e237f-110">Supported user identities</span></span>
<span data-ttu-id="e237f-111">tipos de colecciones diferentes Hello (nube frente a híbrido) admiten el uso de distintas identidades de usuario para acceso tooapplications.</span><span class="sxs-lookup"><span data-stu-id="e237f-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="e237f-112">Para una colección híbrida de RemoteApp, es necesario tooset seguridad de una infraestructura de dominio de Active Directory local y un inquilino de Azure Active Directory con la integración de directorio (y, opcionalmente, inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="e237f-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="e237f-113">Además, es necesario toocreate algunos objetos de Active Directory en el directorio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="e237f-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="e237f-114">Para una colección en la nube de RemoteApp, se puede conceder a cualquier usuario con Azure Active Directory admite identidades de usuario acceso tooRemoteApp tooinclude Accounts de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e237f-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="e237f-115">Vea la siguiente tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e237f-115">See hello table below.</span></span>

<span data-ttu-id="e237f-116">Los usuarios de Office 365 son usuarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e237f-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="e237f-117">Si tienen cuentas de colección híbrida con sincronización de directorios de Azure Active Directory, se les puede conceder acceso de usuario en una implementación híbrida de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e237f-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="e237f-118">Puede utilizar esta tabla como una referencia rápida para el que se admite la identidad en la colección y cuáles son los requisitos de Active Directory de Hola.</span><span class="sxs-lookup"><span data-stu-id="e237f-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="e237f-119">Cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="e237f-119">User accounts</span></span> | <span data-ttu-id="e237f-120">Nube</span><span class="sxs-lookup"><span data-stu-id="e237f-120">Cloud</span></span> | <span data-ttu-id="e237f-121">Híbrida</span><span class="sxs-lookup"><span data-stu-id="e237f-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e237f-122">Cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="e237f-122">Microsoft Account</span></span> |<span data-ttu-id="e237f-123">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-123">Yes</span></span> |<span data-ttu-id="e237f-124">No</span><span class="sxs-lookup"><span data-stu-id="e237f-124">No</span></span> |
| <span data-ttu-id="e237f-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e237f-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="e237f-126">Solo nube de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e237f-126">Azure AD cloud only</span></span> |<span data-ttu-id="e237f-127">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-127">Yes</span></span> |<span data-ttu-id="e237f-128">No</span><span class="sxs-lookup"><span data-stu-id="e237f-128">No</span></span> |
| <span data-ttu-id="e237f-129">ADsync con sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="e237f-129">ADsync with password sync</span></span> |<span data-ttu-id="e237f-130">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-130">Yes</span></span> |<span data-ttu-id="e237f-131">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-131">Yes</span></span> |
| <span data-ttu-id="e237f-132">ADsync sin sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="e237f-132">ADsync without password sync</span></span> |<span data-ttu-id="e237f-133">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-133">Yes</span></span> |<span data-ttu-id="e237f-134">No</span><span class="sxs-lookup"><span data-stu-id="e237f-134">No</span></span> |
| <span data-ttu-id="e237f-135">ADsync con AD FS</span><span class="sxs-lookup"><span data-stu-id="e237f-135">ADsync with AD FS</span></span> |<span data-ttu-id="e237f-136">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-136">Yes</span></span> |<span data-ttu-id="e237f-137">yes</span><span class="sxs-lookup"><span data-stu-id="e237f-137">Yes</span></span> |
| <span data-ttu-id="e237f-138">[Proveedores de identidades de terceros compatibles con Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por ejemplo, Ping)</span><span class="sxs-lookup"><span data-stu-id="e237f-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="e237f-139">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-139">Yes</span></span> |<span data-ttu-id="e237f-140">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-140">Yes</span></span> |
| <span data-ttu-id="e237f-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e237f-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="e237f-142">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-142">Yes</span></span> |<span data-ttu-id="e237f-143">Sí</span><span class="sxs-lookup"><span data-stu-id="e237f-143">Yes</span></span> |

<span data-ttu-id="e237f-144">Consulte [más información](remoteapp-ad.md) sobre cómo configurar Active Directory para RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e237f-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="e237f-145">los usuarios de Azure Active Directory de Hello deben ser de inquilino de Hola que esté asociada con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e237f-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="e237f-146">(Puede ver y modificar su suscripción en hello **configuración** portal Hola de.</span><span class="sxs-lookup"><span data-stu-id="e237f-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="e237f-147">Vea [inquilino de Azure Active Directory de cambio hello usa RemoteApp](remoteapp-changetenant.md) para obtener más información.)</span><span class="sxs-lookup"><span data-stu-id="e237f-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="e237f-148">Información de la cuenta de usuario de Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="e237f-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="e237f-149">Si utilizas Office 365 ProPlus imagen de plantilla hello en la colección de *o* si ha creado una imagen personalizada que usa Office 365, solo se permiten los usuarios de Azure Active Directory tooadd que tienen suscripciones de Office 365 para hello dominio predeterminado de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e237f-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="e237f-150">Consulte [Uso de Office 365 con RemoteApp de Azure](remoteapp-o365.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e237f-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

