---
title: "Azure Active Directory B2C: configuración de WeChat | Microsoft Docs"
description: "Proporcione funciones de registro e inicio de sesión a los consumidores con cuentas de WeChat en las aplicaciones protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="f7450-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los usuarios con cuentas de WeChat</span><span class="sxs-lookup"><span data-stu-id="f7450-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f7450-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="f7450-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="f7450-105">Creación de una aplicación de WeChat</span><span class="sxs-lookup"><span data-stu-id="f7450-105">Create a WeChat application</span></span>

<span data-ttu-id="f7450-106">Para usar WeChat como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de WeChat y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="f7450-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="f7450-107">Necesita una cuenta de WeChat para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="f7450-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="f7450-108">Si no tiene una, puede obtenerla registrándose a través de una de sus aplicaciones móviles o mediante su número de QQ.</span><span class="sxs-lookup"><span data-stu-id="f7450-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="f7450-109">A continuación, registre su cuenta con el programa para desarrolladores de WeChat.</span><span class="sxs-lookup"><span data-stu-id="f7450-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="f7450-110">Puede encontrar más información [aquí](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):</span><span class="sxs-lookup"><span data-stu-id="f7450-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="f7450-111">Registro de una aplicación de WeChat</span><span class="sxs-lookup"><span data-stu-id="f7450-111">Register a WeChat application</span></span>

1. <span data-ttu-id="f7450-112">Vaya a [https://open.weixin.qq.com/](https://open.weixin.qq.com/) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f7450-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="f7450-113">Haga clic en **管理中心** (centro de administración).</span><span class="sxs-lookup"><span data-stu-id="f7450-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="f7450-114">Siga los pasos necesarios para registrar una nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7450-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="f7450-115">Para **授权回调域** (dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f7450-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f7450-116">Por ejemplo, si `tenant_name` es contoso.onmicrosoft.com, establezca la dirección URL para que sea `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f7450-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="f7450-117">Busque y copie el **id. de la aplicación** y la **clave de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f7450-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="f7450-118">Los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f7450-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f7450-119">Configuración de WeChat como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="f7450-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f7450-120">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7450-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="f7450-121">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="f7450-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f7450-122">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="f7450-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="f7450-123">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="f7450-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="f7450-124">Por ejemplo, escriba "WeChat".</span><span class="sxs-lookup"><span data-stu-id="f7450-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="f7450-125">Haga clic en **Tipo de proveedor de identidades**, seleccione **WeChat** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f7450-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="f7450-126">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="f7450-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f7450-127">Escriba la **Clave de la aplicación** que copió anteriormente como **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="f7450-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="f7450-128">Escriba el **Secreto de la aplicación** que copió anteriormente como **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f7450-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="f7450-129">Haga clic en **OK** (Aceptar) y luego en **Create** (Crear) para guardar la configuración de WeChat.</span><span class="sxs-lookup"><span data-stu-id="f7450-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

