---
title: "Azure Active Directory B2C: creación de un inquilino de Azure Active Directory B2C | Microsoft Docs"
description: "Un tema sobre cómo crear un inquilino de Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="ca142-103">Creación de un inquilino de Azure Active Directory B2C en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca142-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="ca142-104">Editar Sipi.</span><span class="sxs-lookup"><span data-stu-id="ca142-104">Edited by Sipi.</span></span>

<span data-ttu-id="ca142-105">Este inicio rápido le ayuda a crear un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ca142-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="ca142-106">Al finalizar, tendrá un inquilino B2C, que podrá usar para registrar aplicaciones B2C.</span><span class="sxs-lookup"><span data-stu-id="ca142-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca142-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca142-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="ca142-108">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="ca142-108">Log in to Azure</span></span>

<span data-ttu-id="ca142-109">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ca142-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="ca142-110">Creación de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ca142-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="ca142-111">Las características B2C no pueden habilitarse en los inquilinos existentes.</span><span class="sxs-lookup"><span data-stu-id="ca142-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="ca142-112">Debe crear un inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca142-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="ca142-113">Enhorabuena, ha creado un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ca142-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="ca142-114">Es administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="ca142-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="ca142-115">Puede agregar otros administradores globales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ca142-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="ca142-116">Para cambiar al nuevo inquilino, haga clic en el *vínculo de administración del nuevo inquilino*.</span><span class="sxs-lookup"><span data-stu-id="ca142-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Vínculo de administración del nuevo inquilino](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="ca142-118">Si planea usar el inquilino B2C para una aplicación de producción, lea el artículo sobre [escala de producción frente a inquilinos de B2C de versión preliminar](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="ca142-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="ca142-119">Existen problemas conocidos al eliminar un inquilino B2C existente y volver a crearlo con el mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="ca142-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="ca142-120">Es necesario crear un inquilino B2C con otro nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="ca142-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="ca142-121">Vinculación del inquilino a la suscripción</span><span class="sxs-lookup"><span data-stu-id="ca142-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="ca142-122">Debe vincular su inquilino de Azure AD B2C a su suscripción a Azure para habilitar todas las funcionalidades de B2C y pagar los cargos por uso.</span><span class="sxs-lookup"><span data-stu-id="ca142-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="ca142-123">Para más información, lea [este artículo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="ca142-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="ca142-124">Si no vincula el inquilino de Azure AD B2C a su suscripción a Azure, se bloquearán algunas funcionalidades y aparecerá un mensaje de advertencia "No Subscription linked to this B2C tenant or the Subscription needs your attention" (No hay ninguna suscripción vinculada con este inquilino de B2C o es necesario revisar la suscripción) en la configuración de B2C.</span><span class="sxs-lookup"><span data-stu-id="ca142-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="ca142-125">Es importante que realice este paso antes de enviar las aplicaciones a producción.</span><span class="sxs-lookup"><span data-stu-id="ca142-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="ca142-126">Acceso sencillo a la configuración</span><span class="sxs-lookup"><span data-stu-id="ca142-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="ca142-127">También puede tener acceso a la hoja escribiendo `Azure AD B2C` en **Buscar recursos** en la parte superior del portal.</span><span class="sxs-lookup"><span data-stu-id="ca142-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="ca142-128">En la lista de resultados, seleccione **Azure AD B2C** para tener acceso a la hoja de configuración de B2C.</span><span class="sxs-lookup"><span data-stu-id="ca142-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca142-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca142-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca142-130">Registro de la aplicación B2C en un inquilino B2C</span><span class="sxs-lookup"><span data-stu-id="ca142-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
