---
title: "Azure Active Directory B2C: configuración de WeChat | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de WeChat en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="f004a-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de WeChat</span><span class="sxs-lookup"><span data-stu-id="f004a-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f004a-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="f004a-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="f004a-105">Creación de una aplicación de WeChat</span><span class="sxs-lookup"><span data-stu-id="f004a-105">Create a WeChat application</span></span>

<span data-ttu-id="f004a-106">toouse WeChat como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de WeChat toocreate y proporcionarla con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f004a-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="f004a-107">Se necesita un toodo de cuenta WeChat.</span><span class="sxs-lookup"><span data-stu-id="f004a-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="f004a-108">Si no tiene una, puede obtenerla registrándose a través de una de sus aplicaciones móviles o mediante su número de QQ.</span><span class="sxs-lookup"><span data-stu-id="f004a-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="f004a-109">A continuación, configurar su cuenta registrado con el programa para desarrolladores de WeChat Hola.</span><span class="sxs-lookup"><span data-stu-id="f004a-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="f004a-110">Puede encontrar más información [aquí](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):</span><span class="sxs-lookup"><span data-stu-id="f004a-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="f004a-111">Registro de una aplicación de WeChat</span><span class="sxs-lookup"><span data-stu-id="f004a-111">Register a WeChat application</span></span>

1. <span data-ttu-id="f004a-112">Vaya demasiado[https://open.weixin.qq.com/](https://open.weixin.qq.com/) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f004a-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="f004a-113">Haga clic en **管理中心** (centro de administración).</span><span class="sxs-lookup"><span data-stu-id="f004a-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="f004a-114">Siga los pasos necesarios de hello tooregister una nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="f004a-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="f004a-115">Para **授权回调域** (dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f004a-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f004a-116">Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f004a-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="f004a-117">Buscar y copia Hola **Id. de aplicación** y **clave de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f004a-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="f004a-118">Los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f004a-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f004a-119">Configuración de WeChat como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="f004a-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f004a-120">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f004a-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="f004a-121">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="f004a-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f004a-122">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="f004a-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="f004a-123">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="f004a-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="f004a-124">Por ejemplo, escriba "WeChat".</span><span class="sxs-lookup"><span data-stu-id="f004a-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="f004a-125">Haga clic en **Tipo de proveedor de identidades**, seleccione **WeChat** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f004a-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="f004a-126">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="f004a-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f004a-127">Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="f004a-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="f004a-128">Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="f004a-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="f004a-129">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de WeChat.</span><span class="sxs-lookup"><span data-stu-id="f004a-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

