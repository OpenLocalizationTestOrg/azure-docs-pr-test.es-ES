---
title: "Azure Active Directory B2C: creación de un inquilino de Azure Active Directory B2C | Microsoft Docs"
description: Un tema en forma de inquilinos toocreate un B2C de Azure Active Directory
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="aca73-103">Crear a un inquilino de Azure Active Directory B2C Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="aca73-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="aca73-104">Editar Sipi.</span><span class="sxs-lookup"><span data-stu-id="aca73-104">Edited by Sipi.</span></span>

<span data-ttu-id="aca73-105">Este inicio rápido le ayuda a crear un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="aca73-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="aca73-106">Cuando haya terminado, tendrá un toouse de inquilino B2C para registrar aplicaciones B2C.</span><span class="sxs-lookup"><span data-stu-id="aca73-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aca73-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aca73-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="aca73-108">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="aca73-108">Log in tooAzure</span></span>

<span data-ttu-id="aca73-109">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aca73-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="aca73-110">Creación de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="aca73-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="aca73-111">Las características B2C no pueden habilitarse en los inquilinos existentes.</span><span class="sxs-lookup"><span data-stu-id="aca73-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="aca73-112">Deberá toocreate un inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aca73-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="aca73-113">Enhorabuena, ha creado un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="aca73-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="aca73-114">Es un administrador Global del inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="aca73-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="aca73-115">Puede agregar otros administradores globales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aca73-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="aca73-116">tooswitch tooyour nuevo inquilino, haga clic en hello *administrar el nuevo vínculo de inquilino*.</span><span class="sxs-lookup"><span data-stu-id="aca73-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Vínculo de administración del nuevo inquilino](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="aca73-118">Si tiene previsto toouse un inquilino B2C para una aplicación de producción, lea el artículo de hello en [producción escala frente a los inquilinos de vista previa B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="aca73-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="aca73-119">Se conocen problemas cuando se elimina un B2C existente de inquilinos y vuelva a crearlo con hello mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="aca73-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="aca73-120">Deberá toocreate un inquilino B2C con un nombre de dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="aca73-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="aca73-121">Vincular su suscripción de inquilino tooyour</span><span class="sxs-lookup"><span data-stu-id="aca73-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="aca73-122">Necesita toolink su AD B2C de Azure inquilino tooyour suscripción de Azure tooenable toda la funcionalidad de B2C y pagar los cargos por uso.</span><span class="sxs-lookup"><span data-stu-id="aca73-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="aca73-123">más información, lea toolearn [este artículo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="aca73-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="aca73-124">Si no vincula su tooyour de inquilino de Azure AD B2C suscripción de Azure, se bloquea alguna funcionalidad y, verá un mensaje de advertencia ("ninguna suscripción vinculados toothis B2C inquilinos u Hola suscripción necesita su atención.") en la configuración de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="aca73-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="aca73-125">Es importante que realice este paso antes de enviar las aplicaciones a producción.</span><span class="sxs-lookup"><span data-stu-id="aca73-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="aca73-126">Acceso fácil toosettings</span><span class="sxs-lookup"><span data-stu-id="aca73-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="aca73-127">También puede tener acceso a hoja Hola escribiendo `Azure AD B2C` en **buscar recursos** en parte superior de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="aca73-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="aca73-128">En la lista de resultados de hello, seleccione **Azure AD B2C** tooaccess Hola B2C hoja de configuración.</span><span class="sxs-lookup"><span data-stu-id="aca73-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aca73-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aca73-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aca73-130">Registro de la aplicación B2C en un inquilino B2C</span><span class="sxs-lookup"><span data-stu-id="aca73-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
