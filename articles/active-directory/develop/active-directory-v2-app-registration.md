---
title: "Registro de una aplicación con el punto de conexión de Azure AD v2.0 mediante el portal | Microsoft Docs"
description: "Cómo registrar una aplicación con Microsoft para habilitar el inicio de sesión y obtener acceso a servicios de Microsoft con el punto de conexión v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="6762c-103">Cómo registrar una aplicación con el punto de conexión v2.0</span><span class="sxs-lookup"><span data-stu-id="6762c-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="6762c-104">Para crear una aplicación que acepte tanto el inicio de sesión de MSA como de Azure AD, tendrá que registrar primero una aplicación con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6762c-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="6762c-105">En este momento, no podrá usar ninguna aplicación existente que tenga con Azure AD o MSA. Tendrá que crear una completamente nueva.</span><span class="sxs-lookup"><span data-stu-id="6762c-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="6762c-106">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="6762c-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="6762c-107">Para determinar si debe usar el punto de conexión v2.0, lea acerca de las [limitaciones de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6762c-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="6762c-108">Visitar el Portal de registro para aplicaciones de Microsoft</span><span class="sxs-lookup"><span data-stu-id="6762c-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="6762c-109">Lo primero es lo primero: vaya a [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="6762c-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="6762c-110">Este es un nuevo portal de registro para aplicaciones donde puede administrar sus aplicaciones de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6762c-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="6762c-111">Inicie sesión con una cuenta personal o una cuenta profesional o educativa de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6762c-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="6762c-112">Si no tiene ninguna de ellas, suscríbase para una nueva cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="6762c-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="6762c-113">Adelante, no le llevará mucho tiempo; aquí le esperamos.</span><span class="sxs-lookup"><span data-stu-id="6762c-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="6762c-114">¿Ha acabado?</span><span class="sxs-lookup"><span data-stu-id="6762c-114">Done?</span></span> <span data-ttu-id="6762c-115">Ahora debería estar viendo su lista de aplicaciones de Microsoft, que probablemente esté vacía.</span><span class="sxs-lookup"><span data-stu-id="6762c-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="6762c-116">Cambiemos eso.</span><span class="sxs-lookup"><span data-stu-id="6762c-116">Let's change that.</span></span>

<span data-ttu-id="6762c-117">Haga clic en **Agregar una aplicación** y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="6762c-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="6762c-118">El portal le asignará a su aplicación un identificador de aplicación único global que usará más adelante en su código.</span><span class="sxs-lookup"><span data-stu-id="6762c-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="6762c-119">Si su aplicación incluye un componente del lado del servidor que necesita tokens de acceso para llamar a las API (como Office, Azure o su propia API web), aquí también le interesará crear un **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="6762c-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="6762c-120">A continuación, agregue las plataformas que usará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6762c-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="6762c-121">Para las aplicaciones basadas en web, proporcione un **URI de redirección** adonde se puedan enviar los mensajes de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6762c-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="6762c-122">Para las aplicaciones móviles, copie el URI de redirección predeterminado creado automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="6762c-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="6762c-123">Si lo desea, puede personalizar la apariencia de la página de inicio de sesión en la sección Perfil.</span><span class="sxs-lookup"><span data-stu-id="6762c-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="6762c-124">Asegúrese de hacer clic en **Guardar** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="6762c-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="6762c-125">Cuando cree una aplicación con [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), la aplicación se registrará en el inquilino principal de la cuenta que use para iniciar sesión en el portal.</span><span class="sxs-lookup"><span data-stu-id="6762c-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="6762c-126">Esto significa que no se puede registrar una aplicación en el inquilino de Azure AD con una cuenta personal de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6762c-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="6762c-127">Si desea registrar explícitamente una aplicación en un inquilino determinado, inicie sesión con una cuenta creada originalmente en ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="6762c-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="6762c-128">Compilar una aplicación de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="6762c-128">Build a quick start app</span></span>
<span data-ttu-id="6762c-129">Ahora que tiene una aplicación de Microsoft, puede completar uno de nuestros tutoriales de inicio rápido de v2.0.</span><span class="sxs-lookup"><span data-stu-id="6762c-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="6762c-130">Estas son algunas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6762c-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

