---
title: "Azure Active Directory B2C: configuración de QQ | Microsoft Docs"
description: "Proporcione funciones de registro e inicio de sesión a los consumidores con cuentas de QQ en las aplicaciones protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="498d3-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los usuarios con cuentas de QQ</span><span class="sxs-lookup"><span data-stu-id="498d3-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="498d3-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="498d3-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="498d3-105">Creación de una aplicación de QQ</span><span class="sxs-lookup"><span data-stu-id="498d3-105">Create a QQ application</span></span>

<span data-ttu-id="498d3-106">Para usar QQ como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Google+ y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="498d3-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="498d3-107">Necesita una cuenta de QQ para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="498d3-107">You need a QQ account to do this.</span></span> <span data-ttu-id="498d3-108">Si no tiene una, puede obtenerla en [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="498d3-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="498d3-109">Registro para el programa para desarrolladores de QQ</span><span class="sxs-lookup"><span data-stu-id="498d3-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="498d3-110">Vaya al [portal para desarrolladores de QQ](http://open.qq.com) e inicie sesión con sus credenciales de cuenta de QQ.</span><span class="sxs-lookup"><span data-stu-id="498d3-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="498d3-111">Después de iniciar sesión, vaya a [http://open.qq.com/reg](http://open.qq.com/reg) para registrarse como un programador.</span><span class="sxs-lookup"><span data-stu-id="498d3-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="498d3-112">En el menú, seleccione**个人** (desarrollador individual).</span><span class="sxs-lookup"><span data-stu-id="498d3-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="498d3-113">Escriba la información necesaria en el formulario y haga clic en **下一步** (paso siguiente).</span><span class="sxs-lookup"><span data-stu-id="498d3-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="498d3-114">Complete el proceso de comprobación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="498d3-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="498d3-115">Debe esperar unos días para recibir la aprobación después de registrarse como desarrollador.</span><span class="sxs-lookup"><span data-stu-id="498d3-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="498d3-116">Registro de una aplicación QQ</span><span class="sxs-lookup"><span data-stu-id="498d3-116">Register a QQ application</span></span>

1. <span data-ttu-id="498d3-117">Vaya a [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="498d3-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="498d3-118">Haga clic en **应用管理** (administración de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="498d3-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="498d3-119">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="498d3-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="498d3-120">Escriba la información de la aplicación necesaria.</span><span class="sxs-lookup"><span data-stu-id="498d3-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="498d3-121">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="498d3-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="498d3-122">Escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="498d3-122">Enter the required information.</span></span>
7. <span data-ttu-id="498d3-123">Para el campo **授权回调域** (dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="498d3-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="498d3-124">Por ejemplo, si `tenant_name` es contoso.onmicrosoft.com, establezca la dirección URL para que sea `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="498d3-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="498d3-125">Haga clic en **创建应用** (crear la aplicación).</span><span class="sxs-lookup"><span data-stu-id="498d3-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="498d3-126">En la página de confirmación, haga clic en **应用管理** (administración de la aplicación) para volver a la página de administración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="498d3-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="498d3-127">Haga clic en **查看** (ver) junto a la aplicación que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="498d3-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="498d3-128">Haga clic en **修改** (editar).</span><span class="sxs-lookup"><span data-stu-id="498d3-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="498d3-129">En la parte superior de la página, copie el **id. de la aplicación** y la **clave de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="498d3-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="498d3-130">Configuración de QQ como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="498d3-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="498d3-131">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="498d3-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="498d3-132">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="498d3-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="498d3-133">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="498d3-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="498d3-134">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="498d3-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="498d3-135">Por ejemplo, escriba "QQ".</span><span class="sxs-lookup"><span data-stu-id="498d3-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="498d3-136">Haga clic en **Tipo de proveedor de identidades**, seleccione **QQ** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="498d3-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="498d3-137">Haga clic en **Configurar este proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="498d3-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="498d3-138">Escriba la **Clave de la aplicación** que copió anteriormente como **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="498d3-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="498d3-139">Escriba el **Secreto de la aplicación** que copió anteriormente como **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="498d3-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="498d3-140">Haga clic en **Aceptar** y luego en **Crear** para guardar la configuración de QQ.</span><span class="sxs-lookup"><span data-stu-id="498d3-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

