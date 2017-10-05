---
title: "Solución de problemas: Elemento \"Active Directory\" falta o no está disponible | Documentos de Microsoft"
description: "Qué hacer cuando el elemento de menú Active Directory no aparece en el Portal de administración de Azure."
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
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="5b603-103">Solución de problemas: El elemento "Active Directory" falta o no está disponible</span><span class="sxs-lookup"><span data-stu-id="5b603-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="5b603-104">Muchas de las instrucciones para usar las características y los servicios de Azure Active Directory comienzan con "Vaya al Portal de administración de Azure y haga clic en **Active Directory**".</span><span class="sxs-lookup"><span data-stu-id="5b603-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="5b603-105">Pero ¿qué hacer si el elemento de menú o la extensión Active Directory no aparecen o están marcados como **No disponible**?</span><span class="sxs-lookup"><span data-stu-id="5b603-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="5b603-106">Este tema está diseñado para ayudarle en este caso.</span><span class="sxs-lookup"><span data-stu-id="5b603-106">This topic is designed to help.</span></span> <span data-ttu-id="5b603-107">Describe las condiciones en que **Active Directory** no aparece o no está disponible y explica cómo proceder.</span><span class="sxs-lookup"><span data-stu-id="5b603-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="5b603-108">Falta Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b603-108">Active Directory is missing</span></span>
<span data-ttu-id="5b603-109">Normalmente, aparece un elemento **Active Directory** en el menú de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="5b603-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="5b603-110">En las instrucciones de procedimientos de Azure Active Directory, se da por supuesto que este elemento aparece en la vista.</span><span class="sxs-lookup"><span data-stu-id="5b603-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Captura de pantalla: Active Directory en Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="5b603-112">El elemento Active Directory se muestra en el menú de navegación izquierdo cuando se dé cualquiera de las siguientes condiciones.</span><span class="sxs-lookup"><span data-stu-id="5b603-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="5b603-113">De lo contrario, el elemento no aparece.</span><span class="sxs-lookup"><span data-stu-id="5b603-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="5b603-114">El usuario actual ha iniciado sesión con una cuenta Microsoft (antes conocida como Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="5b603-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="5b603-115">OR</span><span class="sxs-lookup"><span data-stu-id="5b603-115">OR</span></span>
* <span data-ttu-id="5b603-116">El inquilino de Azure tiene un directorio y la cuenta actual es un administrador de directorio.</span><span class="sxs-lookup"><span data-stu-id="5b603-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="5b603-117">OR</span><span class="sxs-lookup"><span data-stu-id="5b603-117">OR</span></span>
* <span data-ttu-id="5b603-118">El inquilino de Azure tiene al menos un espacio de nombres de Control de acceso de Azure AD (ACS).</span><span class="sxs-lookup"><span data-stu-id="5b603-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="5b603-119">Para obtener más información, consulte [Espacio de nombres de Control de acceso](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b603-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="5b603-120">OR</span><span class="sxs-lookup"><span data-stu-id="5b603-120">OR</span></span>
* <span data-ttu-id="5b603-121">El inquilino de Azure tiene al menos un proveedor de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="5b603-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="5b603-122">Para obtener más información, consulte [Administración de proveedores de Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="5b603-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="5b603-123">Para crear un espacio de nombres de Control de acceso o un proveedor de Multi-Factor Authentication, haga clic en **+Nuevo** > **App Services** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b603-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="5b603-124">Para obtener derechos administrativos a un directorio, pida a un administrador que asigne un rol de administrador a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="5b603-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="5b603-125">Para obtener detalles, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5b603-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="5b603-126">Active Directory no está disponible</span><span class="sxs-lookup"><span data-stu-id="5b603-126">Active Directory is not available</span></span>
<span data-ttu-id="5b603-127">Cuando se hace clic en **+Nuevo** > **App Services**, aparece el elemento **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b603-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="5b603-128">En concreto, el elemento Active Directory aparece cuando cualquiera de las características de Active Directory, como Directorio, Control de acceso o el proveedor de Multi-Factor Authentication, están disponibles para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5b603-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="5b603-129">Sin embargo, mientras se carga la página, el elemento aparece atenuado y marcado como **No disponible**.</span><span class="sxs-lookup"><span data-stu-id="5b603-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="5b603-130">Se trata de un estado temporal.</span><span class="sxs-lookup"><span data-stu-id="5b603-130">This is a temporary state.</span></span> <span data-ttu-id="5b603-131">Si espera unos segundos, el elemento estará disponible.</span><span class="sxs-lookup"><span data-stu-id="5b603-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="5b603-132">Si el retraso se prolonga, el problema se suele resolver cuando se actualiza la página web.</span><span class="sxs-lookup"><span data-stu-id="5b603-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Captura de pantalla: Active Directory no está disponible](./media/active-directory-troubleshooting/not-available.png)

