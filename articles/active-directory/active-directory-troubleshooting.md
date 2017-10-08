---
title: "Solución de problemas: Elemento \"Active Directory\" falta o no está disponible | Documentos de Microsoft"
description: "¿Qué toodo al elemento de menú de Active Directory no aparece en hello Portal de administración de Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="da224-103">Solución de problemas: El elemento "Active Directory" falta o no está disponible</span><span class="sxs-lookup"><span data-stu-id="da224-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="da224-104">Muchas de las instrucciones de hello para el uso de servicios y características de Azure Active Directory comienzan por "toohello Portal de administración de Azure y haga clic en **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="da224-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="da224-105">Pero ¿qué hacer si no aparece el elemento de menú o extensión de Active Directory de Hola o si está marcado como **no está disponible**?</span><span class="sxs-lookup"><span data-stu-id="da224-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="da224-106">Este tema está diseñado toohelp.</span><span class="sxs-lookup"><span data-stu-id="da224-106">This topic is designed toohelp.</span></span> <span data-ttu-id="da224-107">Describe las condiciones de hello en las que **Active Directory** no aparece o no está disponible y se explica cómo tooproceed.</span><span class="sxs-lookup"><span data-stu-id="da224-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="da224-108">Falta Active Directory</span><span class="sxs-lookup"><span data-stu-id="da224-108">Active Directory is missing</span></span>
<span data-ttu-id="da224-109">Normalmente, un **Active Directory** elemento aparece en el menú de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="da224-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="da224-110">instrucciones de Hello en los procedimientos de Azure Active Directory, se supone que este elemento aparece en la vista.</span><span class="sxs-lookup"><span data-stu-id="da224-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Captura de pantalla: Active Directory en Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="da224-112">elemento de Active Directory de Hello aparece en el menú de navegación izquierdo de hello cuando cualquiera de hello condiciones siguientes es verdadera.</span><span class="sxs-lookup"><span data-stu-id="da224-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="da224-113">En caso contrario, el elemento de hello no aparece.</span><span class="sxs-lookup"><span data-stu-id="da224-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="da224-114">usuario actual de Hello iniciado sesión con una cuenta de Microsoft (anteriormente conocida como Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="da224-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="da224-115">OR</span><span class="sxs-lookup"><span data-stu-id="da224-115">OR</span></span>
* <span data-ttu-id="da224-116">Hola inquilino de Azure tiene un directorio y cuenta de hello actual es un administrador de directorios.</span><span class="sxs-lookup"><span data-stu-id="da224-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="da224-117">OR</span><span class="sxs-lookup"><span data-stu-id="da224-117">OR</span></span>
* <span data-ttu-id="da224-118">Hola inquilino de Azure tiene al menos un espacio de nombres de Control de acceso de Azure AD (ACS).</span><span class="sxs-lookup"><span data-stu-id="da224-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="da224-119">Para obtener más información, consulte [Espacio de nombres de Control de acceso](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="da224-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="da224-120">OR</span><span class="sxs-lookup"><span data-stu-id="da224-120">OR</span></span>
* <span data-ttu-id="da224-121">Hola inquilino de Azure tiene al menos un proveedor de autenticación multifactor de Azure.</span><span class="sxs-lookup"><span data-stu-id="da224-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="da224-122">Para obtener más información, consulte [Administración de proveedores de Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="da224-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="da224-123">toocreate un espacio de nombres de Control de acceso o un proveedor de la autenticación multifactor, haga clic en **+ nuevo** > **servicios de aplicaciones** > **deActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="da224-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="da224-124">directorio de tooa de tooget derechos administrativos, haya un administrador asignar a un administrador cuenta tooyour del rol.</span><span class="sxs-lookup"><span data-stu-id="da224-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="da224-125">Para obtener detalles, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="da224-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="da224-126">Active Directory no está disponible</span><span class="sxs-lookup"><span data-stu-id="da224-126">Active Directory is not available</span></span>
<span data-ttu-id="da224-127">Cuando se hace clic en **+Nuevo** > **App Services**, aparece el elemento **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da224-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="da224-128">En concreto, elemento de Active Directory de hello aparece cuando cualquiera de las características de Active Directory de hello, como directorio, Control de acceso o proveedor de autenticación multifactor, están disponibles toohello usuario actual.</span><span class="sxs-lookup"><span data-stu-id="da224-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="da224-129">Sin embargo, mientras se carga la página de hello, elemento de hello aparece atenuado y está marcado como **no está disponible**.</span><span class="sxs-lookup"><span data-stu-id="da224-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="da224-130">Se trata de un estado temporal.</span><span class="sxs-lookup"><span data-stu-id="da224-130">This is a temporary state.</span></span> <span data-ttu-id="da224-131">Si espera unos segundos, el elemento de hello estará disponible.</span><span class="sxs-lookup"><span data-stu-id="da224-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="da224-132">Si se prolonga el retraso de hello, Actualizar página web de Hola a menudo resuelve problema Hola.</span><span class="sxs-lookup"><span data-stu-id="da224-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Captura de pantalla: Active Directory no está disponible](./media/active-directory-troubleshooting/not-available.png)

