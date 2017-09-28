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
ms.openlocfilehash: 8a1d4935397f59e5813afc6f04559e471187a779
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="c66cc-103">Creación de un inquilino de Azure Active Directory B2C en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c66cc-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="c66cc-104">Este inicio rápido le ayuda a crear un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c66cc-104">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="c66cc-105">Al finalizar, tendrá un inquilino B2C, que podrá usar para registrar aplicaciones B2C.</span><span class="sxs-lookup"><span data-stu-id="c66cc-105">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c66cc-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c66cc-106">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="c66cc-107">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="c66cc-107">Log in to Azure</span></span>

<span data-ttu-id="c66cc-108">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c66cc-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="c66cc-109">Creación de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c66cc-109">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="c66cc-110">Las características B2C no pueden habilitarse en los inquilinos existentes.</span><span class="sxs-lookup"><span data-stu-id="c66cc-110">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="c66cc-111">Debe crear un inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c66cc-111">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="c66cc-112">Enhorabuena, ha creado un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c66cc-112">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="c66cc-113">Es administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="c66cc-113">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="c66cc-114">Puede agregar otros administradores globales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c66cc-114">You can add other Global Administrators as required.</span></span> <span data-ttu-id="c66cc-115">Para cambiar al nuevo inquilino, haga clic en el *vínculo de administración del nuevo inquilino*.</span><span class="sxs-lookup"><span data-stu-id="c66cc-115">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Vínculo de administración del nuevo inquilino](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="c66cc-117">Si planea usar el inquilino B2C para una aplicación de producción, lea el artículo sobre [escala de producción frente a inquilinos de B2C de versión preliminar](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="c66cc-117">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="c66cc-118">Existen problemas conocidos al eliminar un inquilino B2C existente y volver a crearlo con el mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="c66cc-118">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="c66cc-119">Es necesario crear un inquilino B2C con otro nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="c66cc-119">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="c66cc-120">Vinculación del inquilino a la suscripción</span><span class="sxs-lookup"><span data-stu-id="c66cc-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="c66cc-121">Debe vincular su inquilino de Azure AD B2C a su suscripción a Azure para habilitar todas las funcionalidades de B2C y pagar los cargos por uso.</span><span class="sxs-lookup"><span data-stu-id="c66cc-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="c66cc-122">Para más información, lea [este artículo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="c66cc-122">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="c66cc-123">Si no vincula el inquilino de Azure AD B2C a su suscripción a Azure, se bloquearán algunas funcionalidades y aparecerá un mensaje de advertencia "No Subscription linked to this B2C tenant or the Subscription needs your attention" (No hay ninguna suscripción vinculada con este inquilino de B2C o es necesario revisar la suscripción) en la configuración de B2C.</span><span class="sxs-lookup"><span data-stu-id="c66cc-123">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="c66cc-124">Es importante que realice este paso antes de enviar las aplicaciones a producción.</span><span class="sxs-lookup"><span data-stu-id="c66cc-124">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="c66cc-125">Acceso sencillo a la configuración</span><span class="sxs-lookup"><span data-stu-id="c66cc-125">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="c66cc-126">También puede tener acceso a la hoja escribiendo `Azure AD B2C` en **Buscar recursos** en la parte superior del portal.</span><span class="sxs-lookup"><span data-stu-id="c66cc-126">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="c66cc-127">En la lista de resultados, seleccione **Azure AD B2C** para tener acceso a la hoja de configuración de B2C.</span><span class="sxs-lookup"><span data-stu-id="c66cc-127">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c66cc-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c66cc-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c66cc-129">Registro de la aplicación B2C en un inquilino B2C</span><span class="sxs-lookup"><span data-stu-id="c66cc-129">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)