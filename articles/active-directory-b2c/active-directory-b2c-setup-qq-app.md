---
title: "Azure Active Directory B2C: configuración de QQ | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de TT en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="c0a82-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de TT</span><span class="sxs-lookup"><span data-stu-id="c0a82-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="c0a82-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c0a82-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="c0a82-105">Creación de una aplicación de QQ</span><span class="sxs-lookup"><span data-stu-id="c0a82-105">Create a QQ application</span></span>

<span data-ttu-id="c0a82-106">toouse TT como proveedor de identidades en Azure Active Directory (Azure AD) B2C, que necesita una aplicación TT toocreate y proporcionarla con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0a82-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="c0a82-107">Se necesita un toodo de cuenta TT.</span><span class="sxs-lookup"><span data-stu-id="c0a82-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="c0a82-108">Si no tiene una, puede obtenerla en [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="c0a82-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="c0a82-109">Registrarse para el programa de desarrolladores de hello TT</span><span class="sxs-lookup"><span data-stu-id="c0a82-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="c0a82-110">Vaya toohello [portal para desarrolladores de TT](http://open.qq.com) e inicie sesión con sus credenciales de cuenta TT.</span><span class="sxs-lookup"><span data-stu-id="c0a82-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="c0a82-111">Después de iniciar sesión, vaya demasiado[http://open.qq.com/reg](http://open.qq.com/reg) tooregister usted como desarrollador.</span><span class="sxs-lookup"><span data-stu-id="c0a82-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="c0a82-112">En el menú de hello, seleccione**个人**(para desarrolladores individuales).</span><span class="sxs-lookup"><span data-stu-id="c0a82-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="c0a82-113">Introducir información de hello necesario en el formulario de Hola y haga clic en**下一步**(paso siguiente).</span><span class="sxs-lookup"><span data-stu-id="c0a82-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="c0a82-114">Complete el proceso de comprobación de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0a82-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="c0a82-115">Necesitará toowait unos toobe días aprobado después de registrar como desarrollador.</span><span class="sxs-lookup"><span data-stu-id="c0a82-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="c0a82-116">Registro de una aplicación QQ</span><span class="sxs-lookup"><span data-stu-id="c0a82-116">Register a QQ application</span></span>

1. <span data-ttu-id="c0a82-117">Vaya demasiado[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="c0a82-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="c0a82-118">Haga clic en **应用管理** (administración de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="c0a82-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="c0a82-119">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="c0a82-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="c0a82-120">Escriba la información de aplicación necesarios Hola.</span><span class="sxs-lookup"><span data-stu-id="c0a82-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="c0a82-121">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="c0a82-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="c0a82-122">Escriba la información de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="c0a82-122">Enter hello required information.</span></span>
7. <span data-ttu-id="c0a82-123">Para hello**授权回调域**(dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="c0a82-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="c0a82-124">Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="c0a82-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="c0a82-125">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="c0a82-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="c0a82-126">En la página de confirmación de hello, haga clic en**应用管理**página de administración de aplicaciones de toohello de tooreturn de (administración de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="c0a82-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="c0a82-127">Haga clic en**查看**aplicación toohello siguiente (vista) que se acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="c0a82-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="c0a82-128">Haga clic en **修改** (editar).</span><span class="sxs-lookup"><span data-stu-id="c0a82-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="c0a82-129">Desde la parte superior de la página de Hola Hola copiar hello **Id. de aplicación** y **clave de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c0a82-130">Configuración de QQ como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="c0a82-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c0a82-131">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a82-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="c0a82-132">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c0a82-133">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0a82-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="c0a82-134">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="c0a82-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="c0a82-135">Por ejemplo, escriba "QQ".</span><span class="sxs-lookup"><span data-stu-id="c0a82-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="c0a82-136">Haga clic en **Tipo de proveedor de identidades**, seleccione **QQ** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="c0a82-137">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="c0a82-138">Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="c0a82-139">Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="c0a82-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="c0a82-140">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de TT.</span><span class="sxs-lookup"><span data-stu-id="c0a82-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

