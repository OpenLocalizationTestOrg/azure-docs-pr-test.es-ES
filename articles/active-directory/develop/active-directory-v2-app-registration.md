---
title: "una aplicación con el punto de conexión de v2.0 de hello Azure AD mediante el portal de hello aaaRegister | Documentos de Microsoft"
description: "Cómo tooregister una aplicación con Microsoft para habilitar el inicio de sesión y acceder a Microsoft services utilizando el punto de conexión de hello v2.0"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="3543c-103">¿Cómo tooregister una aplicación con el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="3543c-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="3543c-104">toobuild una aplicación que acepta MSA & Azure AD iniciar sesión, primero deberá tooregister una aplicación con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3543c-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="3543c-105">En este momento, no ser capaz de toouse las aplicaciones existentes que pueda tener con Azure AD o MSA - deberá toocreate una marca de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3543c-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="3543c-106">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="3543c-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="3543c-107">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3543c-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="3543c-108">Visite el portal de registro de aplicación de Microsoft de Hola</span><span class="sxs-lookup"><span data-stu-id="3543c-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="3543c-109">Lo primero es lo primero: Navegue demasiado[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="3543c-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="3543c-110">Este es un nuevo portal de registro para aplicaciones donde puede administrar sus aplicaciones de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3543c-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="3543c-111">Inicie sesión con una cuenta personal o una cuenta profesional o educativa de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3543c-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="3543c-112">Si no tiene ninguna de ellas, suscríbase para una nueva cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="3543c-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="3543c-113">Adelante, no le llevará mucho tiempo; aquí le esperamos.</span><span class="sxs-lookup"><span data-stu-id="3543c-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="3543c-114">¿Ha acabado?</span><span class="sxs-lookup"><span data-stu-id="3543c-114">Done?</span></span> <span data-ttu-id="3543c-115">Ahora debería estar viendo su lista de aplicaciones de Microsoft, que probablemente esté vacía.</span><span class="sxs-lookup"><span data-stu-id="3543c-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="3543c-116">Cambiemos eso.</span><span class="sxs-lookup"><span data-stu-id="3543c-116">Let's change that.</span></span>

<span data-ttu-id="3543c-117">Haga clic en **Agregar una aplicación** y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="3543c-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="3543c-118">portal de Hello asignará a la aplicación un identificador único global de aplicación que va a utilizar más adelante en el código.</span><span class="sxs-lookup"><span data-stu-id="3543c-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="3543c-119">Si la aplicación incluye un componente de servidor que necesita tokens de acceso para llamar a las API (pensar: Office, Azure o su propia API web), le interesará toocreate una **secreto de aplicación** aquí también.</span><span class="sxs-lookup"><span data-stu-id="3543c-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="3543c-120">A continuación, agregue Hola plataformas que se va a usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3543c-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="3543c-121">Para las aplicaciones basadas en web, proporcione un **URI de redirección** adonde se puedan enviar los mensajes de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3543c-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="3543c-122">Para las aplicaciones móviles, copia profundidad predeterminada de hello crea automáticamente de uri de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="3543c-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="3543c-123">Si lo desea, puede personalizar Hola apariencia y comportamiento de la página de inicio de sesión en hello perfil.</span><span class="sxs-lookup"><span data-stu-id="3543c-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="3543c-124">Asegúrese de que tooclick **guardar** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="3543c-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="3543c-125">Cuando se crea una aplicación con [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), se registrará la aplicación hello en particular inquilinos de Hola de cuenta de hello que usa toosign en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3543c-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="3543c-126">Esto significa que no se puede registrar una aplicación en el inquilino de Azure AD con una cuenta personal de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3543c-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="3543c-127">Si explícitamente desea tooregister una aplicación en un inquilino determinado, inicie sesión con una cuenta que se creó originalmente en ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="3543c-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="3543c-128">Compilar una aplicación de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="3543c-128">Build a quick start app</span></span>
<span data-ttu-id="3543c-129">Ahora que tiene una aplicación de Microsoft, puede completar uno de nuestros tutoriales de inicio rápido de v2.0.</span><span class="sxs-lookup"><span data-stu-id="3543c-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="3543c-130">Estas son algunas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3543c-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

