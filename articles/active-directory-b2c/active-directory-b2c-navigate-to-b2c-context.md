---
title: 'Azure Active Directory B2C: cambio a inquilino B2C | Microsoft Docs'
description: "Cómo se cambia de inquilino de Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="fc94b-103">Cambio a inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fc94b-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="fc94b-104">Para configurar Azure AD B2C, debe estar con el inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fc94b-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="fc94b-105">Inicio de sesión en el inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fc94b-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="fc94b-106">Para ir hasta el inquilino de Azure AD B2C, debe haber iniciado sesión en Azure Portal como administrador global del inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fc94b-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="fc94b-107">Inicie sesión en el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc94b-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="fc94b-108">Para cambiar el inquilino, haga clic en la dirección de correo electrónico o la imagen de la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="fc94b-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="fc94b-109">En la lista `Directory` que aparece, seleccione el inquilino de Azure AD B2C que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="fc94b-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="fc94b-110">Azure Portal se actualizará.</span><span class="sxs-lookup"><span data-stu-id="fc94b-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="fc94b-111">Ahora estará conectado en Azure Portal al inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fc94b-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="fc94b-112">Navegación a la hoja de características B2C</span><span class="sxs-lookup"><span data-stu-id="fc94b-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="fc94b-113">Haga clic en **Examinar** en el panel de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="fc94b-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="fc94b-114">Haga clic en **> Más servicios** y busque `Azure AD B2C` en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="fc94b-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="fc94b-115">(Para anclar al panel de inicio izquierdo, haga clic en la estrella a la izquierda de Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="fc94b-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="fc94b-116">Haga clic en **Azure AD B2C** para tener acceso a la hoja de características de B2C.</span><span class="sxs-lookup"><span data-stu-id="fc94b-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Captura de pantalla de la hoja de características de B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="fc94b-118">Necesita ser administrador global del inquilino B2C para poder acceder a la hoja Características B2C.</span><span class="sxs-lookup"><span data-stu-id="fc94b-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="fc94b-119">Un administrador global de cualquier otro inquilino o un usuario de cualquier inquilino no puede acceder a dicha hoja.</span><span class="sxs-lookup"><span data-stu-id="fc94b-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="fc94b-120">Puede cambiar a su inquilino B2C mediante el selector de inquilinos de la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fc94b-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
