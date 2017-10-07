---
title: "Azure Active Directory B2C: configuración de Weibo | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Weibo en las aplicaciones que están protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="8241f-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Weibo</span><span class="sxs-lookup"><span data-stu-id="8241f-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="8241f-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="8241f-104">This feature is in preview.</span></span> <span data-ttu-id="8241f-105">No utilice este proveedor de identidades en su entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8241f-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="8241f-106">Creación de una aplicación de Weibo</span><span class="sxs-lookup"><span data-stu-id="8241f-106">Create a Weibo application</span></span>

<span data-ttu-id="8241f-107">toouse Weibo como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Weibo toocreate y proporcionarla con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="8241f-108">Se necesita un toodo de cuenta Weibo.</span><span class="sxs-lookup"><span data-stu-id="8241f-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="8241f-109">Si no tiene una, puede obtenerla en [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="8241f-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="8241f-110">Registrarse para el programa de desarrolladores de hello Weibo</span><span class="sxs-lookup"><span data-stu-id="8241f-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="8241f-111">Vaya toohello [portal para desarrolladores de Weibo](http://open.weibo.com/) e inicie sesión con sus credenciales de cuenta Weibo.</span><span class="sxs-lookup"><span data-stu-id="8241f-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="8241f-112">Después de iniciar sesión, haga clic en el nombre para mostrar en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="8241f-113">En la lista desplegable de hello, seleccione**编辑开发者信息**(editar la información para desarrolladores).</span><span class="sxs-lookup"><span data-stu-id="8241f-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="8241f-114">Introducir información de hello necesario en el formulario de Hola y haga clic en**提交**(enviar).</span><span class="sxs-lookup"><span data-stu-id="8241f-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="8241f-115">Complete el proceso de comprobación de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="8241f-116">Vaya toohello [página de comprobación de identidad](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="8241f-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="8241f-117">Introducir información de hello necesario en el formulario de Hola y haga clic en**提交**(enviar).</span><span class="sxs-lookup"><span data-stu-id="8241f-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="8241f-118">Registro de una aplicación de Weibo</span><span class="sxs-lookup"><span data-stu-id="8241f-118">Register a Weibo application</span></span>

1. <span data-ttu-id="8241f-119">Vaya toohello [nueva página de registro de aplicación de Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="8241f-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="8241f-120">Escriba la información de aplicación necesaria Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="8241f-121">Haga clic en **创建** (crear).</span><span class="sxs-lookup"><span data-stu-id="8241f-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="8241f-122">Copiar valores de hello de **clave de aplicación** y **secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="8241f-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="8241f-123">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="8241f-123">You will need this later.</span></span>
5. <span data-ttu-id="8241f-124">Cargar fotografías Hola necesario y escriba la información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="8241f-125">Haga clic en **保存以上信息** (guardar).</span><span class="sxs-lookup"><span data-stu-id="8241f-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="8241f-126">Haga clic en **高级信息** (información avanzada).</span><span class="sxs-lookup"><span data-stu-id="8241f-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="8241f-127">Haga clic en**编辑**(Editar) siguiente campo toohello para OAuth2.0**授权设置**(dirección URL de redireccionamiento).</span><span class="sxs-lookup"><span data-stu-id="8241f-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="8241f-128">Escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para OAuth2.0 **授权设置** (dirección URL de redireccionamiento).</span><span class="sxs-lookup"><span data-stu-id="8241f-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="8241f-129">Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="8241f-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="8241f-130">Haga clic en **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="8241f-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="8241f-131">Configuración de Weibo como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="8241f-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="8241f-132">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8241f-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="8241f-133">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="8241f-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="8241f-134">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8241f-135">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="8241f-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="8241f-136">Por ejemplo, escriba "Weibo".</span><span class="sxs-lookup"><span data-stu-id="8241f-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="8241f-137">Haga clic en **Tipo de proveedor de identidades**, seleccione **Weibo** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8241f-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="8241f-138">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="8241f-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="8241f-139">Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="8241f-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="8241f-140">Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="8241f-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="8241f-141">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Weibo.</span><span class="sxs-lookup"><span data-stu-id="8241f-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

