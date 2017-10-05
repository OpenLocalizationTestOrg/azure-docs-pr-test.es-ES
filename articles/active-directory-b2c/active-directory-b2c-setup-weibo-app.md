---
title: "Azure Active Directory B2C: configuración de Weibo | Microsoft Docs"
description: "Proporcione funciones de registro e inicio de sesión a los consumidores con cuentas de Weibo en las aplicaciones protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="0f6b7-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los usuarios con cuentas de Weibo</span><span class="sxs-lookup"><span data-stu-id="0f6b7-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0f6b7-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-104">This feature is in preview.</span></span> <span data-ttu-id="0f6b7-105">No utilice este proveedor de identidades en su entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="0f6b7-106">Creación de una aplicación de Weibo</span><span class="sxs-lookup"><span data-stu-id="0f6b7-106">Create a Weibo application</span></span>

<span data-ttu-id="0f6b7-107">Para usar Weibo como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Weibo y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="0f6b7-108">Necesita una cuenta de Weibo para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="0f6b7-109">Si no tiene una, puede obtenerla en [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="0f6b7-110">Registro para el programa para desarrolladores de Weibo</span><span class="sxs-lookup"><span data-stu-id="0f6b7-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="0f6b7-111">Vaya al [portal para desarrolladores de Weibo](http://open.weibo.com/) e inicie sesión con sus credenciales de cuenta de Weibo.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="0f6b7-112">Después de iniciar sesión, haga clic en el nombre para mostrar en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="0f6b7-113">En la lista desplegable, seleccione **编辑开发者信息** (editar la información para desarrolladores).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="0f6b7-114">Escriba la información necesaria en el formulario y haga clic en **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="0f6b7-115">Complete el proceso de comprobación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="0f6b7-116">Vaya a la [página de comprobación de identidad](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="0f6b7-117">Escriba la información necesaria en el formulario y haga clic en **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="0f6b7-118">Registro de una aplicación de Weibo</span><span class="sxs-lookup"><span data-stu-id="0f6b7-118">Register a Weibo application</span></span>

1. <span data-ttu-id="0f6b7-119">Vaya a la [página de registro de la aplicación de Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="0f6b7-120">Escriba la información de aplicación necesaria.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="0f6b7-121">Haga clic en **创建** (crear).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="0f6b7-122">Copie los valores de **Clave de la aplicación** y **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="0f6b7-123">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-123">You will need this later.</span></span>
5. <span data-ttu-id="0f6b7-124">Cargue las fotos y escriba la información necesarias.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="0f6b7-125">Haga clic en **保存以上信息** (guardar).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="0f6b7-126">Haga clic en **高级信息** (información avanzada).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="0f6b7-127">Haga clic en **编辑** (editar) junto al campo de OAuth2.0 **授权设置** (dirección URL de redireccionamiento).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="0f6b7-128">Escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para OAuth2.0 **授权设置** (dirección URL de redireccionamiento).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="0f6b7-129">Por ejemplo, si `tenant_name` es contoso.onmicrosoft.com, establezca la dirección URL para que sea `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="0f6b7-130">Haga clic en **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="0f6b7-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0f6b7-131">Configuración de Weibo como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="0f6b7-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0f6b7-132">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="0f6b7-133">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0f6b7-134">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0f6b7-135">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="0f6b7-136">Por ejemplo, escriba "Weibo".</span><span class="sxs-lookup"><span data-stu-id="0f6b7-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="0f6b7-137">Haga clic en **Tipo de proveedor de identidades**, seleccione **Weibo** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="0f6b7-138">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="0f6b7-139">Escriba la **Clave de la aplicación** que copió anteriormente como **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="0f6b7-140">Escriba el **Secreto de la aplicación** que copió anteriormente como **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="0f6b7-141">Haga clic en **OK** (Aceptar) y luego en **Create** (Crear) para guardar la configuración de Weibo.</span><span class="sxs-lookup"><span data-stu-id="0f6b7-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

